<template>
 <v-content>
      <v-container
        class="fill-height"
        fluid
      >
<v-row
align="center"
          justify="center"
>

    <p class="text-center display-3">Введіть свій емейл</p>
</v-row>
       
        <v-row
          align="center"
          justify="center"
        >
    
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
           
              
            
                <v-form v-model="valid" lazy-validation ref="form">
                  <v-text-field
                  color="secondary"
                    name="login"
                    v-model="email"
                    type="text"
                    placeholder="Email"
                    :rules="emailRules"
                  />
                  
                </v-form>
              
                 
                  

              
              <v-card-actions class="mt-4 bts">
                  <v-btn class="nr ml-2" text  to="/" color="secondary">Закрити</v-btn>
                <v-btn   class="nr elevation-0 mr-2 disabled white--text" @click="recover" depressed color="rgb(20, 19, 19)" :disabled="valid===false" >Продовжити</v-btn>
              </v-card-actions>
            
          </v-col>
        </v-row>
      </v-container>
    </v-content>
</template>
<script>
export default {


    data() {
        return {
            email:'',
            valid:false,
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
            ]
        }
        
    },
    methods: {
     recover(){
if (this.$refs.form.validate()){
    this.$store.dispatch('recoverUser',this.email)
    .then(
        ()=>{  
            this.$router.push('/')
        }
    )
    .catch(
        
        err=>console.log('err',err))
    

}

        }
    }
}
</script>

<style scoped>
.nr{
border-radius: 0px;

}
.cc{
    padding: 0
}
.nr:first-child{
    border: 1px solid gray;
}
.v-text-field__details{
display: none !important;
}
.v-messages{
    display: none !important;
}
.pa{
    padding: 0px;
}
.sz{
    font-size: 12px;
}
.pr{
    display: flex;
    justify-content: space-between;
}

.bts{
    justify-content: center;
    
}
</style>