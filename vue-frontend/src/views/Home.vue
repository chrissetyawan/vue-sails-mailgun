<template>

  <div class="home pt-4">
    
    <div class="forms ">

      <div class="content">
        <label for="" class="label-form">Sender</label>
        <div class="row">
          <div class="col">
            <input autofocus type="text" v-model="sender_name" class="form-control input" placeholder="Sender Name">
          </div>
          <div class="col">
            <input type="text" v-model="sender_email" class="form-control input" placeholder="Sender Email">
          </div>
        </div>

        <label for="" class="label-form mt-4">Recipient</label>
        <div class="row">
          <div class="col">
            <input type="text" v-model="recipient_name" class="form-control input" placeholder="Recipient Name">
          </div>
          <div class="col">
            <input type="text" v-model="recipient_email" class="form-control input" placeholder="Recipient Email">
          </div>
        </div>

        <label for="" class="label-form mt-4">Message</label>
        <div class="row">
          <div class="col">
            <textarea v-model="message" class="form-control input" placeholder="Write message"></textarea>
          </div>
        </div>
      </div>

      <hr class="line"/>
      
      <div class="row footer">
        <div class="col-md-5">
          <button v-on:click="submitForm" class="btn button-submit w-100">SUBMIT</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src
import Vue from 'vue'
import Axios from 'axios'

export default {
  name: 'Home',
  data: function(){
    return {
      sender_name: '',
      sender_email: '',
      recipient_email: '',
      recipient_name: '',
      message: '',
    }
  },
  methods: {
    submitForm(){
      if(!this.sender_name || !this.sender_email || !this.recipient_email || !this.recipient_name || !this.message){
        Vue.$toast.success('⚠ Data error, you shall not pass',{
          type: 'error'
        })
      }else{
        if(!/\S+@\S+\.\S+/.test(this.sender_email) || !/\S+@\S+\.\S+/.test(this.recipient_email)){
          Vue.$toast.success('⚠ Email must be valid',{
          type: 'error'
        })
        }else{

          Axios.post('http://localhost:1337/data',{
            sender_name: this.sender_name,
            sender_email: this.sender_email,
            recipient_email: this.recipient_email,
            recipient_name: this.recipient_name,
            message: this.message,
          }).then(e=>{
            if(e.data.isError == '0'){
              Vue.$toast.success('✅ Data confirmed, you may proceed',{
          type: 'success'
        })
            }else{
              Vue.$toast.success('⚠ Oops!! Something went wrong with server.',{
          type: 'danger'
        })
            }

            this.sender_name = ''
            this.sender_email = ''
            this.recipient_email = ''
            this.recipient_name = ''
            this.message = ''
          })

          
        }
        
      }
    }
  }
}
</script>


<style lang="scss">
.home{
  display: flex;
  justify-content: center;
  padding-bottom: 2rem;
}
.input{
  color: white !important;
  background-color: #3D3B44 !important;
  box-sizing: border-box;
  border: 2px solid #666175 !important;
  padding: 20px 10px !important;
  border-radius: 6px;
}
.input::placeholder{
  color: #666175 !important;
  font-size: bold;
}
.input:focus::placeholder{
  color: white !important;
}
.form-control:focus{
  box-shadow: 0 0 0 0.1rem rgba(255,255,255,1);
}
.row {
  display: flex;
  flex-direction: row;
}
.forms{
  background-color: #323234;
  color: white;
  width: 636px;
  border: 1px solid #434246;
  box-sizing: border-box;
  border-radius: 6px;
}
.label-form{
  font-family: Lato;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 29px;
  /* identical to box height */
  display: flex;
  align-items: center;
  /* Yellow 4 */
  color: #FFCA63;
}
button:focus {
    outline: blue auto 5px; 
}
.button-submit{
  background-color: #7A5DD1;
  color: white;
  font-weight: bold;
  border: 2px solid #FFFFFF;
  border-radius: 8px;
}
.button-submit:active{
  background-color: #5B41A8;
  color: white;
  outline: none;
}
.button-submit:hover{
  color: white !important;
}
.btn.focus, .btn:focus {
    outline: 0;
    box-shadow: none;
}
.line {
  border-top: 1px solid #434246;
  margin-top: 0px;
  margin-bottom: 0px;
}
.content {
  padding: 20px;
}
.footer {
  padding: 20px;
}
@media only screen and (max-width: 768px) {
  .home{
    /* padding-top: 1rem;
    padding-bottom: 2rem; */
    padding: 25px;
  }
  .forms {
    width: 100%;
  }
  .content {
    padding: 15px;
  }
  .row {
    flex-direction: column;
  }
  .input{
    width: 100%;
    margin-bottom: 10px;
  }
}
</style>
