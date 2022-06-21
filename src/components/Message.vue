<template>

<div class="message-group">
    <div class="spinner"></div>
    <div class="message">"{{ message }}"</div>
</div> 

</template>

<script>
export default {
    name: "Message",
    props:{
        message: String
    }
}
</script>

<style lang="scss" scoped>
    .message-group{
        font-size: 28px;
        font-weight: 800;
        margin: 1.5rem 0;
        transition: height 0.4s;

        @media (max-width: 450px){ font-size: 22px; margin: 1rem 0;}

        .spinner {
            border: 8px solid rgba(0, 0, 0, 0.1);
            border-left-color: var(--NeonGreen);
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: auto;

        }

        .spinner,
        .message{
            &.d-none{
                display: none;
            }

        }

        @keyframes spin {
            to {
                transform: rotate(360deg);
            }
        }
    }
</style>