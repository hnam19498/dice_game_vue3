<template>
    <div class="wrapper-popup" :class="getClassPopup">
        <div class="rule">
            <h3>Luật chơi</h3>
            <p>Nội dung luật chơi</p>
            <button class="confirm" @click="offPopup">Ok</button>
        </div>
    </div>
</template>
<script>
export default {
    methods: {
        offPopup() {
            this.$emit('handleOffPopup')
        }
    },
    props: {
        isOpenPopup: { type: Boolean, default: false }
    },
    data() {
        return {}
    },
    computed: {
        getClassPopup: function () {
            return { 'open-popup': this.isOpenPopup }
        }
    }
}
</script>
<style>
.wrapper-popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
    transition: all .3s ease;
}

.wrapper-popup.open-popup {
    opacity: 1;
    visibility: visible;
}

.open-popup .rule {
    transform: scale(1) translate(-50%, -50%);
}

.rule {
    position: absolute;
    background-color: white;
    width: 400px;
    top: 50%;
    transition: all .3s ease;
    padding: 20px;
    font-family: Arial, Helvetica, sans-serif;
    left: 50%;
    transform: scale(1.2) translate(-50%, -50%);
}

.rule h3 {
    margin-bottom: 10px;
}

.rule .confirm {
    cursor: pointer;
    margin-top: 20px;
    padding: 8px 15px;
    border: 2px solid black;
    background-color: white;
    float: right;
    transition: all 0.3s ease;
}

.confirm:hover {
    background-color: green;
    color: white;
}
</style>