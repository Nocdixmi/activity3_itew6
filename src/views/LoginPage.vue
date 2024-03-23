<template>
    <div>
        <h1>Login Page</h1>
        <button @click="handleClick">Login</button>
    </div>
</template>

<script>
export default {
    methods: {
        handleClick() {
            localStorage.setItem('token', '12345')
            this.$router.push({ name: 'products' })
        }
    }
}
</script>