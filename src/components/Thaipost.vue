<template>
    <div class="container">
        <div class="row">
            <div class="col-11"><b-form-input v-model="track" size="lg" placeholder="ตัวอย่าง : EF582568151TH"></b-form-input></div>
            <b-button @click='getToken()' pill variant="outline-danger">search</b-button>
        </div>
        <div class="row mt-3">
            <div class="col-md-12">
                <b-card v-if="msg != null"
                
                :title= "_track"
                tag="article" >

           <b-list-group>
               <h4>Status : </h4>
               <b-list-group-item v-for = "list in msg"
               :key="list.bar">
                   <h4> {{list.status_description}}  : {{list.status_date}} </h4>
               </b-list-group-item>

           </b-list-group>
                <h4>ผู้รับ : {{receiver}}</h4><br>
                <a v-bind:href="singnature" target="_blank"><h4>singnature</h4></a>        
            </b-card> 
            </div>
             
        </div>

    </div>

</template>

<script>
import axios from'axios'
export default {
    data(){
        return{
            msg : null,
            tokencate : 'Token'+ ' ' + 'X2DkV+NtQvBbC4D=JlKjTHBuCKV8L3PYRcH-DZYzR=QIDkYnO=T=OKRGHZW0RGGICGATTyUJVxY+P^A4ROEcVVFyTuRCUyV^IrZz',
            barcode : [],
            token:'',
            track: "",
            receiver : null,
            count : null,
            singnature : null,
            
        }
    }
    ,
    methods :{
        getToken(){
            let config = {
                headers:{
                    'Authorization' : this.tokencate,
                    'Content-Type': 'application/json'
                }
            }
            let data = {
                'HTTP_CONTENT_LANGUAGE': self.language
            }
            axios.post('https://trackapi.thailandpost.co.th/post/api/v1/authenticate/token',data, config)
            .then(response => {
               
                this.token = 'Token' + ' ' + response.data.token
                this.getItem()
                
            })

            
        },

        getItem(){
            let config = {
                headers:{
                    'Authorization' : this.token,
                    'Content-Type': 'application/json'
                }
            }
            var data = JSON.stringify({"status":"all","language":"TH","barcode":[this.track]});
            
            
            axios.post('https://trackapi.thailandpost.co.th/post/api/v1/track',data,config)
            .then(response => {
                
                this.msg = Object.values(response.data.response.items)
                this.msg = Object.values(this.msg[0])

                this.count = Object.keys(this.msg).length - 1;
                this.receiver = this.msg[this.count].receiver_name
                this.singnature = this.msg[this.count].signature
                this._track =this.track
                console.log(this.msg)
            })
            .catch( (err)=> {
                    console.log(err)
                }
            )
        }
    }

}
</script>

<style>


</style>