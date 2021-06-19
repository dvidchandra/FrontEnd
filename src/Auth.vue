<template>
    <div>
        <div>
            <p>Username : </p>
            <input type="text" v-model="username"/>
        </div>
        <div>
            <p>Password : </p>
            <input type="password" v-model="password">
        </div>
        
        <button @click="save">Save</button>
        <button @click="deleted"> Delete</button>
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
        this.username = localStorage.getItem('user')
        this.password = localStorage.getItem('pwd')
    },
    methods:{
        save : function (){
            localStorage.setItem('user',this.username)
            localStorage.setItem('pwd',this.password)
        },
        deleted : function (){
            localStorage.removeItem('user',this.username)
            localStorage.removeItem('pwd',this.password)
            this.username = ''
            this.password = ''
        }
    }
}
</script>

<style scoped>

</style>