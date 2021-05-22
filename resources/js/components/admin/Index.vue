<template>
  <div>
    <admin-main></admin-main>

    <div class="content-wrapper">
      <section class="content-header">
        <h1>Analysis</h1>
        <ol class="breadcrumb">
          <li>
            <a href="#"><i class="fa fa-dashboard"></i>Home</a>
          </li>
          <li class="active">Dashboard</li>
        </ol>
      </section>
      <h1 v-if="loading" style="text-align: center; font-size: 50px">
        <i class="fa fa-spinner fa-spin"></i>
      </h1>
      <section v-else class="content">

        <div class="row" v-if="$can('manage order')">

          <div class="col-lg-3 col-xs-6">
            <div class="small-box bg-green">
              <div class="inner">
                <h3 class="">{{ orders.new_order }}</h3>
                <h4>New Member</h4>
              </div>
              <div class="icon"></div>
              <router-link :to="{ name: 'NewOrder' }" class="small-box-footer"
                >More info <i class="fa fa-arrow-circle-right"></i
              ></router-link>
            </div>
          </div>

        </div>

        <div class="row">
          <h1 style="margin-left: 15px" v-if="$can('manage accounts')">Accounts</h1>
          <div class="col-lg-3">
            <div class="custom-box">
              <div class="custom-box-body">
                <h4>
                  In Cash: <strong>{{ parseInt(balance.today_credit_cash) }}</strong>
                </h4>
                <h4>
                  In Bkash(personal):
                  <strong>{{ parseInt(balance.today_credit_bkash_personal) }}</strong>
                </h4>
                <h4>
                  In Bkash(merchant):
                  <strong>{{ parseInt(balance.today_credit_bkash_merchant) }}</strong>
                </h4>
                <h4>
                  In Bank: <strong>{{ parseInt(balance.today_credit_bank) }}</strong>
                </h4>

                <h4>
                  Total: <strong>{{ parseInt(balance.today_credit) }}</strong>
                </h4>
              </div>

              <div class="custom-box-footer">
                <h3 class="text-center text-uppercase">today credit</h3>
              </div>
            </div>
          </div>
          <div class="col-lg-3">
            <div class="custom-box">
              <div class="custom-box-body">
                <h4>
                  In Cash: <strong>{{ parseInt(balance.today_debitt_cash) }}</strong>
                </h4>
                <h4>
                  In Bkash(personal):
                  <strong>{{ parseInt(balance.today_debit_bkash_personal) }}</strong>
                </h4>
                <h4>
                  In Bkash(merchant):
                  <strong>{{ parseInt(balance.today_debit_bkash_merchant) }}</strong>
                </h4>
                <h4>
                  In Bank: <strong>{{ parseInt(balance.today_debit_bank) }}</strong>
                </h4>

                <h4>
                  Total: <strong>{{ parseInt(balance.today_debit) }}</strong>
                </h4>
              </div>

              <div class="custom-box-footer">
                <h3 class="text-center text-uppercase">today debit</h3>
              </div>
            </div>
          </div>
          <!-- <div class="col-lg-3">
            <div class="custom-box">
              <div class="custom-box-body">
                  <h4>In Cash: <strong>{{parseInt(balance.total_credit_cash)}}</strong></h4>
                  <h4>In Bkash(personal): <strong>{{ parseInt(balance.total_credit_bkash_personal) }}</strong></h4>
                  <h4>In Bkash(merchant): <strong>{{ parseInt(balance.total_credit_bkash_merchant) }}</strong></h4>
                   <h4>In Bank: <strong>{{parseInt(balance.total_credit_bank)}}</strong></h4>
                     <h4>Total: <strong>{{parseInt(balance.total_credit)}}</strong></h4>

              </div>

              <div class="custom-box-footer">
                <h3 class="text-center text-uppercase">total credit</h3>
              </div>
            </div>
          </div>
          <div class="col-lg-3">
            <div class="custom-box">
              <div class="custom-box-body">
                  <h4>In Cash: <strong>{{parseInt(balance.total_debitt_cash)}}</strong></h4>
                  <h4>In Bkash(personal): <strong>{{ parseInt(balance.total_debit_bkash_personal) }}</strong></h4>
                  <h4>In Bkash(merchant): <strong>{{ parseInt(balance.total_debit_bkash_merchant) }}</strong></h4>
                   <h4>In Bank: <strong>{{parseInt(balance.total_debit_bank)}}</strong></h4>
                  <h4>Total: <strong>{{parseInt(balance.total_debit)}}</strong></h4>

              </div>

              <div class="custom-box-footer">
                <h3 class="text-center text-uppercase">total debit</h3>
              </div>
            </div>
          </div> -->

          <!-- <div class="col-lg-3">
            <div class="custom-box">
              <div class="custom-box-body">
                  <h4>In Cash: <strong>{{parseInt(balance.today_credit_cash)-parseInt(balance.today_debitt_cash)}}</strong></h4>
                  <h4>In Bkash(personal): <strong>{{ parseInt(balance.today_credit_bkash_personal)- parseInt(balance.today_debit_bkash_personal)}}</strong></h4>
                  <h4>In Bkash(merchant): <strong>{{ parseInt(balance.today_credit_bkash_merchant)-parseInt(balance.today_debit_bkash_merchant) }}</strong></h4>
                   <h4>In Bank: <strong>{{parseInt(balance.today_credit_bank)-parseInt(balance.today_debit_bank)}}</strong></h4>
                   <h4>Total: <strong>{{parseInt(balance.today_credit)-parseInt(balance.today_debit)}}</strong></h4>

              </div>

              <div class="custom-box-footer">
                <h3 class="text-center text-uppercase">today balance</h3>
              </div>
            </div>
          </div> -->

          <div class="col-lg-3">
            <div class="custom-box">
              <div class="custom-box-body">
                <h4>
                  In Cash:
                  <strong>{{
                    parseInt(balance.total_credit_cash) -
                    parseInt(balance.total_debitt_cash)
                  }}</strong>
                </h4>
                <h4>
                  In Bkash(personal):
                  <strong>{{
                    parseInt(balance.total_credit_bkash_personal) -
                    parseInt(balance.total_debit_bkash_personal)
                  }}</strong>
                </h4>
                <h4>
                  In Bkash(merchant):
                  <strong>{{
                    parseInt(balance.total_credit_bkash_merchant) -
                    parseInt(balance.total_debit_bkash_merchant)
                  }}</strong>
                </h4>
                <h4>
                  In Bank:
                  <strong>{{
                    parseInt(balance.total_credit_bank) -
                    parseInt(balance.total_debit_bank)
                  }}</strong>
                </h4>

                <h4>
                  Total:
                  <strong>{{
                    parseInt(balance.total_credit) - parseInt(balance.total_debit)
                  }}</strong>
                </h4>
              </div>

              <div class="custom-box-footer">
                <h3 class="text-center text-uppercase">total balance</h3>
              </div>
            </div>
          </div>
        </div>

        <div class="row" v-if="$can('manage accounts')">

          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-12">
                <h1 style="text-align: right; margin-top: 30px">Analysis</h1>

                <div class="custom-box">
                  <div class="custom-box-body">
                    <ul class="analysis-item">
                      <li
                        :class="{ active: analysisshow == 1 }"
                        @click="analysisshow = 1"
                      >
                        Today
                      </li>
                      <li
                        :class="{ active: analysisshow == 2 }"
                        @click="analysisshow = 2"
                      >
                        This week
                      </li>
                      <li
                        :class="{ active: analysisshow == 3 }"
                        @click="analysisshow = 3"
                      >
                        This Month
                      </li>
                    </ul>
                    <table class="table table-striped table-hover table-bordered ">
                      <thead>
                        <tr>
                          <td></td>
                          <td>O.Qty</td>
                          <td>P.Qty</td>
                          <td>Amount</td>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="(item,index) in analysis" :key="index">
                          <td>{{index}}</td>
                          <td>

                                <span v-if="analysisshow == 1">
                                  {{item.today.order_quantity}}
                                </span>
                                 <span v-if="analysisshow == 2">
                                  {{item.this_week.order_quantity}}
                                </span>
                                 <span v-if="analysisshow == 3">
                                  {{item.this_month.order_quantity}}
                                </span>

                            </td>
                             <td>

                                <span v-if="analysisshow == 1">
                                  {{item.today.product_quanity}}
                                </span>
                                 <span v-if="analysisshow == 2">
                                  {{item.this_week.product_quanity}}
                                </span>
                                 <span v-if="analysisshow == 3">
                                  {{item.this_month.product_quanity}}
                                </span>

                            </td>
                             <td>

                                <span v-if="analysisshow == 1">
                                  {{item.today.amount}}
                                </span>
                                 <span v-if="analysisshow == 2">
                                  {{item.this_week.amount}}
                                </span>
                                 <span v-if="analysisshow == 3">
                                  {{item.this_month.amount}}
                                </span>

                            </td>

                        </tr>
                         <tr>


                          <td></td>
                          <td>
                            <span> = <b v-if="analysisshow == 1">
                                {{ parseInt( analysis.sale.today.order_quantity
                                  ? analysis.sale.today.order_quantity
                                  : 0)+  parseInt( analysis.wholesale.today.order_quantity
                                  ? analysis.wholesale.today.order_quantity
                                  : 0)+ parseInt( analysis.order.today.order_quantity
                                  ? analysis.order.today.order_quantity
                                  : 0)}}
                                  </b>

                                   <b v-if="analysisshow == 2">
                                {{ parseInt( analysis.sale.this_week.order_quantity
                                  ? analysis.sale.this_week.order_quantity
                                  : 0)+  parseInt( analysis.wholesale.this_week.order_quantity
                                  ? analysis.wholesale.this_week.order_quantity
                                  : 0)+ parseInt( analysis.order.this_week.order_quantity
                                  ? analysis.order.this_week.order_quantity
                                  : 0)}}

                                   </b>
                                    <b v-if="analysisshow == 3">
                                {{ parseInt( analysis.sale.this_month.order_quantity
                                  ? analysis.sale.this_month.order_quantity
                                  : 0)+  parseInt( analysis.wholesale.this_month.order_quantity
                                  ? analysis.wholesale.this_month.order_quantity
                                  : 0)+ parseInt( analysis.order.this_month.order_quantity
                                  ? analysis.order.this_month.order_quantity
                                  : 0)}}

                                    </b>

                              </span>
                          </td>
                             <td>
                            <span> = <b v-if="analysisshow == 1">
                                {{ parseInt( analysis.sale.today.product_quanity
                                  ? analysis.sale.today.product_quanity
                                  : 0)+  parseInt( analysis.wholesale.today.product_quanity
                                  ? analysis.wholesale.today.product_quanity
                                  : 0)+ parseInt( analysis.order.today.product_quanity
                                  ? analysis.order.today.product_quanity
                                  : 0)}}
                                  </b>

                                   <b v-if="analysisshow == 2">
                                {{ parseInt( analysis.sale.this_week.product_quanity
                                  ? analysis.sale.this_week.product_quanity
                                  : 0)+  parseInt( analysis.wholesale.this_week.product_quanity
                                  ? analysis.wholesale.this_week.product_quanity
                                  : 0)+ parseInt( analysis.order.this_week.product_quanity
                                  ? analysis.order.this_week.product_quanity
                                  : 0)}}

                                   </b>
                                    <b v-if="analysisshow == 3">
                                {{ parseInt( analysis.sale.this_month.product_quanity
                                  ? analysis.sale.this_month.product_quanity
                                  : 0)+  parseInt( analysis.wholesale.this_month.product_quanity
                                  ? analysis.wholesale.this_month.product_quanity
                                  : 0)+ parseInt( analysis.order.this_month.product_quanity
                                  ? analysis.order.this_month.product_quanity
                                  : 0)}}

                                    </b>

                              </span>
                          </td>
                              <td>
                            <span> = <b v-if="analysisshow == 1">
                                {{ parseInt( analysis.sale.today.amount
                                  ? analysis.sale.today.amount
                                  : 0)+  parseInt( analysis.wholesale.today.amount
                                  ? analysis.wholesale.today.amount
                                  : 0)+ parseInt( analysis.order.today.amount
                                  ? analysis.order.today.amount
                                  : 0)}}
                                  </b>

                                   <b v-if="analysisshow == 2">
                                {{ parseInt( analysis.sale.this_week.amount
                                  ? analysis.sale.this_week.amount
                                  : 0)+  parseInt( analysis.wholesale.this_week.amount
                                  ? analysis.wholesale.this_week.amount
                                  : 0)+ parseInt( analysis.order.this_week.amount
                                  ? analysis.order.this_week.amount
                                  : 0)}}

                                   </b>
                                    <b v-if="analysisshow == 3">
                                {{ parseInt( analysis.sale.this_month.amount
                                  ? analysis.sale.this_month.amount
                                  : 0)+  parseInt( analysis.wholesale.this_month.amount
                                  ? analysis.wholesale.this_month.amount
                                  : 0)+ parseInt( analysis.order.this_month.amount
                                  ? analysis.order.this_month.amount
                                  : 0)}}

                                    </b>

                              </span>
                          </td>

                        </tr>


                        <!-- <tr>
                          <td>OfficeSale</td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.sale.today.order_quantity
                                  ? analysis.sale.today.order_quantity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.sale.this_week.order_quantity
                                  ? analysis.sale.this_week.order_quantity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.sale.this_month.order_quantity
                                  ? analysis.sale.this_month.order_quantity
                                  : 0
                              }}</b
                            >
                          </td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.sale.today.product_quanity
                                  ? analysis.sale.today.product_quanity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.sale.this_week.product_quanity
                                  ? analysis.sale.this_week.product_quanity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.sale.this_month.product_quanity
                                  ? analysis.sale.this_month.product_quanity
                                  : 0
                              }}</b
                            >
                          </td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.sale.today.amount
                                  ? analysis.sale.today.amount
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.sale.this_week.amount
                                  ? analysis.sale.this_week.amount
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.sale.this_month.amount
                                  ? analysis.sale.this_month.amount
                                  : 0
                              }}</b
                            >
                          </td>
                        </tr>

                        <tr>
                          <td>Wholesale</td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.wholesale.today.order_quantity
                                  ? analysis.wholesale.today.order_quantity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.wholesale.this_week.order_quantity
                                  ? analysis.wholesale.this_week.order_quantity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.wholesale.this_month.order_quantity
                                  ? analysis.wholesale.this_month.order_quantity
                                  : 0
                              }}</b
                            >
                          </td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.wholesale.today.product_quanity
                                  ? analysis.wholesale.today.product_quanity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.wholesale.this_week.product_quanity
                                  ? analysis.wholesale.this_week.product_quanity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.wholesale.this_month.product_quanity
                                  ? analysis.wholesale.this_month.product_quanity
                                  : 0
                              }}</b
                            >
                          </td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.wholesale.today.amount
                                  ? analysis.wholesale.today.amount
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.wholesale.this_week.amount
                                  ? analysis.wholesale.this_week.amount
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.wholesale.this_month.amount
                                  ? analysis.wholesale.this_month.amount
                                  : 0
                              }}</b
                            >
                          </td>
                        </tr>

                        <tr>
                          <td>order</td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.order.today.order_quantity
                                  ? analysis.order.today.order_quantity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.order.this_week.order_quantity
                                  ? analysis.order.this_week.order_quantity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.order.this_month.order_quantity
                                  ? analysis.order.this_month.order_quantity
                                  : 0
                              }}</b
                            >
                          </td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.order.today.product_quanity
                                  ? analysis.order.today.product_quanity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.order.this_week.product_quanity
                                  ? analysis.order.this_week.product_quanity
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.order.this_month.product_quanity
                                  ? analysis.order.this_month.product_quanity
                                  : 0
                              }}</b
                            >
                          </td>

                          <td>
                            <b v-if="analysisshow == 1">
                              {{
                                analysis.order.today.amount
                                  ? analysis.order.today.amount
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 2">
                              {{
                                analysis.order.this_week.amount
                                  ? analysis.order.this_week.amount
                                  : 0
                              }}
                            </b>
                            <b v-if="analysisshow == 3">
                              {{
                                analysis.order.this_month.amount
                                  ? parseInt(analysis.order.this_month.amount)
                                  : 0
                              }}</b
                            >
                          </td>
                        </tr>

                        <tr>


                          <td></td>
                          <td>
                            <span> = <b v-if="analysisshow == 1">
                                {{ parseInt( analysis.sale.today.order_quantity
                                  ? analysis.sale.today.order_quantity
                                  : 0)+  parseInt( analysis.wholesale.today.order_quantity
                                  ? analysis.wholesale.today.order_quantity
                                  : 0)+ parseInt( analysis.order.today.order_quantity
                                  ? analysis.order.today.order_quantity
                                  : 0)}}
                                  </b>

                                   <b v-if="analysisshow == 2">
                                {{ parseInt( analysis.sale.this_week.order_quantity
                                  ? analysis.sale.this_week.order_quantity
                                  : 0)+  parseInt( analysis.wholesale.this_week.order_quantity
                                  ? analysis.wholesale.this_week.order_quantity
                                  : 0)+ parseInt( analysis.order.this_week.order_quantity
                                  ? analysis.order.this_week.order_quantity
                                  : 0)}}

                                   </b>
                                    <b v-if="analysisshow == 3">
                                {{ parseInt( analysis.sale.this_month.order_quantity
                                  ? analysis.sale.this_month.order_quantity
                                  : 0)+  parseInt( analysis.wholesale.this_month.order_quantity
                                  ? analysis.wholesale.this_month.order_quantity
                                  : 0)+ parseInt( analysis.order.this_month.order_quantity
                                  ? analysis.order.this_month.order_quantity
                                  : 0)}}

                                    </b>

                              </span>
                          </td>
                             <td>
                            <span> = <b v-if="analysisshow == 1">
                                {{ parseInt( analysis.sale.today.product_quanity
                                  ? analysis.sale.today.product_quanity
                                  : 0)+  parseInt( analysis.wholesale.today.product_quanity
                                  ? analysis.wholesale.today.product_quanity
                                  : 0)+ parseInt( analysis.order.today.product_quanity
                                  ? analysis.order.today.product_quanity
                                  : 0)}}
                                  </b>

                                   <b v-if="analysisshow == 2">
                                {{ parseInt( analysis.sale.this_week.product_quanity
                                  ? analysis.sale.this_week.product_quanity
                                  : 0)+  parseInt( analysis.wholesale.this_week.product_quanity
                                  ? analysis.wholesale.this_week.product_quanity
                                  : 0)+ parseInt( analysis.order.this_week.product_quanity
                                  ? analysis.order.this_week.product_quanity
                                  : 0)}}

                                   </b>
                                    <b v-if="analysisshow == 3">
                                {{ parseInt( analysis.sale.this_month.product_quanity
                                  ? analysis.sale.this_month.product_quanity
                                  : 0)+  parseInt( analysis.wholesale.this_month.product_quanity
                                  ? analysis.wholesale.this_month.product_quanity
                                  : 0)+ parseInt( analysis.order.this_month.product_quanity
                                  ? analysis.order.this_month.product_quanity
                                  : 0)}}

                                    </b>

                              </span>
                          </td>
                              <td>
                            <span> = <b v-if="analysisshow == 1">
                                {{ parseInt( analysis.sale.today.amount
                                  ? analysis.sale.today.amount
                                  : 0)+  parseInt( analysis.wholesale.today.amount
                                  ? analysis.wholesale.today.amount
                                  : 0)+ parseInt( analysis.order.today.amount
                                  ? analysis.order.today.amount
                                  : 0)}}
                                  </b>

                                   <b v-if="analysisshow == 2">
                                {{ parseInt( analysis.sale.this_week.amount
                                  ? analysis.sale.this_week.amount
                                  : 0)+  parseInt( analysis.wholesale.this_week.amount
                                  ? analysis.wholesale.this_week.amount
                                  : 0)+ parseInt( analysis.order.this_week.amount
                                  ? analysis.order.this_week.amount
                                  : 0)}}

                                   </b>
                                    <b v-if="analysisshow == 3">
                                {{ parseInt( analysis.sale.this_month.amount
                                  ? analysis.sale.this_month.amount
                                  : 0)+  parseInt( analysis.wholesale.this_month.amount
                                  ? analysis.wholesale.this_month.amount
                                  : 0)+ parseInt( analysis.order.this_month.amount
                                  ? analysis.order.this_month.amount
                                  : 0)}}

                                    </b>

                              </span>
                          </td>

                        </tr> -->
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>



      </section>
    </div>
  </div>
</template>

<script>
import carousel from "vue-owl-carousel";

export default {
  name: "Index",

  data() {
    return {
      orders: {},
      loading: true,
      due: "",
      balance: {},
      stock: "",
      admin_orders: "",
      top_selling_products_today: "",
      base_url: this.$store.state.image_base_link,
      analysis: "",
      analysisshow: 1,
    };
  },
  created() {},
  mounted() {
    this.$store.dispatch("admin");
    this.dashboard();
  },
  methods: {
    dashboard() {
      axios
        .get("/dashboard")
        .then((resp) => {
          console.log(resp);
          this.orders = resp.data.orders;
          this.balance = resp.data.balance;
          this.stock = resp.data.stock;
          this.admin_orders = resp.data.admin_order;
          this.top_selling_products_today = resp.data.top_selling_products_today;
          this.analysis = resp.data.analysis;
          this.due = resp.data.due;
          this.loading = false;

          //  console.log(resp.data.stock)
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },

  components: {
    carousel,
  },
  computed: {
    admin() {
      return this.$store.getters.admin;
    },
  },
};
</script>

<style>
.box-gradiant {
  background: -webkit-linear-gradient(to right, #c33764, #1d2671);
  background: linear-gradient(to right, #c33764, #1d2671);
}
.small-box .icon {
  color: #fff !important;
  opacity: 0.6;
}
.product-thumb.clearfix {
  padding: 12px 13px;
  margin-right: 10px;
  margin-right: 10px;
  border: 1px solid #eee;
  box-shadow: 2px 2px 2px #eee;
}
.custom-box {
  background: #fff;
  padding: 13px;
  height: 280px;
  box-shadow: 3px 3px 3px #ddd;
  border-radius: 6px;
  margin-bottom: 10px;

}
.custom-box-body strong {
  position: absolute;
  right: 10%;
  color: blue;
}
.custom-box-footer {
  background: #00a65a;
  color: #fff;
}
.analysis-item {
  display: flex;
  list-style-type: none;
  float: right;
}
.analysis-item li {
  padding: 10px 10px;
  text-transform: uppercase;
  font-weight: bold;
  cursor: pointer;
}
.analysis-item .active {
  border-bottom: 2px solid #000;
}
</style>
