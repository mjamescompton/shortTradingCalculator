<template>
    <div class="tt-calc tt-calc--short container">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <div class="card card-default">
                    <div class="card-header"><h4>Short Trading Calculator</h4></div>
                    <div class="card-body">
                        <form>
                          <div class="form-group">
                            <label for="amount">Coin Amount</label>
                            <input v-on:keyup="update" v-model="amount" type="number" class="form-control" id="amount" step="0.00000001" value="0">
                          </div>
                          <div class="form-group">
                            <label for="sell-price">Sell Price</label>
                            <input v-on:keyup="update" v-model="sell" type="number" class="form-control" id="sell-price" step="0.00000001" value="0">
                          </div>
                          <div class="form-group">
                            <label for="buy-price">Buy Price</label>
                            <input v-on:keyup="update" v-model="buy" type="number" class="form-control" id="buy-price" step="0.00000001" value="0">
                          </div>
                        </form>
                        <p><b>Total Coins: </b>{{total}}</p>
                        <p><b>Profit/Loss: </b>{{profit}}</p>
                        <p><b>Trading Fee: </b></p>
                        <p><b>Profit Percentage: </b><input style="width:30%;display: inline;" v-on:keyup="updatePercent" v-model="percentage" type="number" class="form-control" id="buy-price" step=" 1" value="0">%</p>
                    </div>

                </div>
            </div>
        </div>
    </div>

</template>

<script>
  export default {
    data: function() {
        return {
            amount: '0',
            sell: '0',
            buy: '0',
            total: '0',
            profit: '0',
            percentage: '0'
          }
    },
    mounted() {
      console.log('Component mounted.');
    },      
    methods: {
      update: function() {
        // ( Amount x Sell ) / Buy = ( Amount + Profit )  
        if ( this.amount > 0 && this.sell > 0 && this.buy > 0 ) {
          this.total = ( this.amount * this.sell ) / this.buy;
          this.profit = this.total - this.amount;
          this.percentage = parseFloat( 100 * this.profit / this.amount).toFixed(2);
        }
      },
      updatePercent: function() {

        if ( this.amount > 0 && this.sell > 0 ) {
          this.buy = ( this.sell / ( +this.percentage + +100 ) ) * 100
          this.total = ( this.amount * this.sell ) / this.buy;
          this.profit = this.total - this.amount;

        }

      }
    }
  }
</script>
