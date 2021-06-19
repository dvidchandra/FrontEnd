<template>
    <div>
        <div>
            <label >Username : </label>
            <input type="text" v-model="username"/>
        </div>
        <div>
            <label >Password : </label>
            <input type="password" v-model="password">
        </div>
        
        <button @click="simpan">Save</button>
        <button @click="hapus"> Delete</button>
    </div>
</template>

<script>
export default {
    data : function() {
        return {
            username : '',
            password : ''
        }
    },
    created:function(){
        this.username = localStorage.getItem('usr')
        this.password = localStorage.getItem('pwd')
    },
    methods:{
        simpan : function (){
            localStorage.setItem('usr',this.username)
            localStorage.setItem('pwd',this.password)
        },
        hapus : function (){
            localStorage.removeItem('usr',this.username)
            localStorage.removeItem('pwd',this.password)
            this.username = ''
            this.password = ''
        }
    }
}
</script>

<style scoped>

</style>