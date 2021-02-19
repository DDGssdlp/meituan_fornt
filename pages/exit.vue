<template>
  <div class=""/>
</template>

<script>
export default {
  layout: 'blank',
   async mounted(){
      
    let loginUserPhone = localStorage.getItem("loginUser");
      await this.$axios.get('/auth/exit', { params:{
        loginUserPhone
      }}).then(res => {
          console.log("res", res)
          this.$router.push("/")
            localStorage.removeItem("loginUser")     
      }).catch(err =>{
        this.$router.push("/")
      })
   },

  middleware: async (ctx) => {
    
   
  }
}
</script>
