<template>
    <div container v-if="status == '1'">
        <div class="row">
            <div class="col-md-12">
                <table width="100%" style="margin-top: 1px; padding: 0;background-color: #E32126 ">
                    <tr style="padding:0; margin: 0">
                        <td width="20%;" height="60px;"></td>
                        <td width="300px;"  align="center" class="fontKanti fontS18" style="cursor: pointer;padding:0px;margin:0px; color: white;" >
                            <router-link to="/cake">
                                <button class="btn btn-outline-light" style="width:100%;height:60px;margin:0px;border-radius:0px;">CAKE</button>
                            </router-link>
                        </td>
                        <td width="300px;" align="center" class="fontKanti fontS18" style="cursor: pointer;padding:0px;margin:0px; color: white;" >
                            
                            <router-link to="/drink">
                                <button class="btn btn-outline-light" style="width:100%;height:60px;margin:0px;border-radius:0px;">DRINK</button>
                            </router-link>                        </td>
                        <td width="300px;" align="center" class="fontKanti fontS18" style="cursor:pointer;padding:0px;margin:0px; color: white;" >
                            <router-link to="/cookie">
                                <button class="btn btn-outline-light" style="width:100%;height:60px;margin:0px;border-radius:0px;">COOKIES</button>
                            </router-link>    
                        </td>
                        <td width="20%;" height="60px;"></td>
                    </tr>
        </table>
            </div>
        </div>
        
    </div> 
    <div>
        test
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data(){
        return{
            products: [],
            status:'1',
            p_id: "",
            p_name: "",
            p_price: 0,
            stock: 0,
            category: "",
            p_detail: "",
            num:1,

            prod:{
                p_id: "C005",
                p_name: "sab",
                p_price: 300,
                stock: 3,
                category: "nueng",
                p_detail: "nueng",
            },
            iid:''
            ,
            use:{}
        }
    },
    created(){
        let apiURL = 'http://mcafe.app.ruk-com.cloud/api/';
        axios.get(apiURL).then(res => {
            this.products = res.data
        }).catch(error => {
            console.log(error)
        });
        let apIURL = `http://mcafe.app.ruk-com.cloud/api/edit-Users/${this.$route.params.id}`;
        axios.get(apIURL).then((res) => {
            this.user = res.data
        }).catch(error => {
            console.log(error)
        });
    },
    methods:{
        send_id(pro){
            this.status = '2';
            this.p_id=pro.p_id;
            this.p_name= pro.p_name;
            this.p_price= pro.p_price;
            this.stock= pro.stock;
            this.category=pro.category;
            this.p_detail=pro.p_detail;
            this.iid=pro._id;
        },
        deUnit(){
            if(this.num > 1){
                this.num -= 1;
            }
        },
        addUnit(){
            if(this.num < this.stock){
                this.num += 1;
            }
        },
        updated(id){
            console.log(id)
            this.prod.p_id= this.p_id;
            this.prod.p_name= this.p_name;
            this.prod.p_price= 300;
            this.prod.stock= this.stock-this.num;
            this.prod.category= this.category;
            this.prod.p_detail= this.p_detail;
            let apiURL = `http://mcafe.app.ruk-com.cloud/api/update-product/${id}`;
                axios.put(apiURL, this.prod).then((res) => {
                    console.log(res);
                    this.$router.push('/')
                }).catch(error => {
                    console.log(error)
                })
        }
    }
}
</script>