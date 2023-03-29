<template>
  <div>
    <v-autocomplete
      dense
      clearable
      auto-select-first
      outlined
      color="primary"
      :label="frappe._('Customer')"
      v-model="customer"
      :items="customers"
      item-text="customer_name"
      item-value="name"
      background-color="white"
      :no-data-text="__('Customer not found')"
      hide-details
      :filter="customFilter"
      :disabled="readonly"
      append-icon="mdi-plus"
      @click:append="new_customer"
      prepend-inner-icon="mdi-account-edit"
      @click:prepend-inner="edit_customer"
    >
      <template v-slot:item="data">
        <template>
          <v-list-item-content>
            <v-list-item-title
              class="primary--text subtitle-1"
              v-html="data.item.customer_name"
            ></v-list-item-title>
            <v-list-item-subtitle
              v-if="data.item.customer_name != data.item.name"
              v-html="`ID: ${data.item.name}`"
            ></v-list-item-subtitle>
            <v-list-item-subtitle
              v-if="data.item.tax_id"
              v-html="`TAX ID: ${data.item.tax_id}`"
            ></v-list-item-subtitle>
            <v-list-item-subtitle
              v-if="data.item.email_id"
              v-html="`Email: ${data.item.email_id}`"
            ></v-list-item-subtitle>
            <v-list-item-subtitle
              v-if="data.item.mobile_no"
              v-html="`Mobile No: ${data.item.mobile_no}`"
            ></v-list-item-subtitle>
            <v-list-item-subtitle
              v-if="data.item.primary_address"
              v-html="`Primary Address: ${data.item.primary_address}`"
            ></v-list-item-subtitle>
          </v-list-item-content>
        </template>
      </template>
    </v-autocomplete>
    <v-autocomplete
      dense
      clearable
      auto-select-first
      outlined
      class="painter"
      color="primary"
      :label="frappe._('Painter')"
      v-model="painter"
      :items="painters"
      item-value="name"
      background-color="white"
      item-text="name"
      :filter="painterFilter"
      :no-data-text="__('Painter not found')"
      hide-details
      :disabled="readonly"
     
    >
    <template v-slot:item="data">
              <template>
                <v-list-item-content>
                  <v-list-item-title
                  class="painter_search"
                    v-html="data.item.name"
                  ></v-list-item-title>
                </v-list-item-content>
              </template>
            </template>
    </v-autocomplete>
    
  </div>
</template>

<script>
import { evntBus } from '../../bus';
export default {
  data: () => ({
    pos_profile: '',
    painter:'',
    customers: [],
    painters:[],
    customer: '',
    readonly: false,
  }),

  methods: {
    get_painter_names() {
     
      const vm = this;
      frappe.call({
        method: 'posawesome.posawesome.api.posapp.painter_list',
        args: {},
        callback: function (r) {
         
          if (r.message) {
            r.message.forEach((element) => {
                vm.painters.push({"name":element.name});
              });
            }}
      });
    },
    get_customer_names() {
      const vm = this;
      if (vm.pos_profile.posa_local_storage && localStorage.customer_storage) {
        vm.customers = JSON.parse(localStorage.getItem('customer_storage'));
      }
      frappe.call({
        method: 'posawesome.posawesome.api.posapp.get_customer_names',
        args: {
          pos_profile: this.pos_profile.pos_profile,
        },
        callback: function (r) {
        
          if (r.message) {
        
            vm.customers = r.message;
            console.info('loadCustomers');
            if (vm.pos_profile.posa_local_storage) {
              localStorage.setItem('customer_storage', '');
              localStorage.setItem(
                'customer_storage',
                JSON.stringify(r.message)
              );
            }
          }
        },
      });
    },
    new_customer() {
      evntBus.$emit('open_new_customer');
    },
    edit_customer() {
      evntBus.$emit('open_edit_customer');
    },
    customFilter(item, queryText, itemText) {
      const textOne = item.customer_name
        ? item.customer_name.toLowerCase()
        : '';
      const paintertext = item.painter_name ? item.painter_name.toLowerCase() : '';
      const textTwo = item.tax_id ? item.tax_id.toLowerCase() : '';
      const textThree = item.email_id ? item.email_id.toLowerCase() : '';
      const textFour = item.mobile_no ? item.mobile_no.toLowerCase() : '';
      const textFifth = item.name.toLowerCase();
      const searchText = queryText.toLowerCase();

      return (
        textOne.indexOf(searchText) > -1 ||
        paintertext.indexOf(searchText) > -1 ||
        textTwo.indexOf(searchText) > -1 ||
        textThree.indexOf(searchText) > -1 ||
        textFour.indexOf(searchText) > -1 ||
        textFifth.indexOf(searchText) > -1
      );
    },
  },
  PainterFilter(item, queryText, itemText) {
      const textOne = item.name.toLowerCase();
      const searchText = queryText.toLowerCase();
      return textOne.indexOf(searchText) > -1;
    },
  computed: {},

  created: function () {
    this.$nextTick(function () {
      evntBus.$on('register_pos_profile', (pos_profile) => {
        this.pos_profile = pos_profile;
        this.get_customer_names();
        this.get_painter_names();
      });
      evntBus.$on('set_customer', (customer) => {
       
        this.customer = customer;
      });

      evntBus.$on('add_customer_to_list', (customer) => {
        this.customers.push(customer);
      });
      evntBus.$on('set_painter', (painter) => {
        this.painter = painters;
      });
      evntBus.$on('add_painter_to_list', (painter) => {
        this.painters.push(painter);
      });
      evntBus.$on('set_customer_readonly', (value) => {
        this.readonly = value;
      });
    
    });
  },

  watch: {
    customer() {
      evntBus.$emit('update_customer', this.customer);
    },
    painter(){
      evntBus.$emit('update_painter', this.painter);
    }
  },
};
</script>

<style>
.painter{
  padding-top: 12px !important;
};

</style>