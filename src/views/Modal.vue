<template>
    <div>
        {{title}}
        <hr>
        <a href="#id01">Open Modal</a>
        <div id="id01" class="modal">
            <div class="modal-dialog">
                <header class="container">
                    <a href="#" class="closebtn" >x</a>
                    <h2>Modal Header</h2>
                </header>
                <div class="container">
                    <p> some text1</p>
                    <p> some text2</p>
                </div>
                <footer class="container">
                    <p>Modal footer</p>

                </footer>

            </div>

        </div>
    </div>    
</template>

<script>
export default {
    name: 'Modal',
    data() {
        return {
            title: 'Hello1'
        }
    },
    props: [],
    methods: {

    }
}
</script>

<style scoped>
@keyframes example {
    from {top: -100px; opacity: 0;}
    to {top: 0px; opacity: 1;}
}

header {
    background-color: cadetblue;
}
footer {
    background-color: cadetblue;
}

.modal {
    display: none;
    overflow: auto;
    width: 80%;
    height: 100%;
    overflow: auto;
    left: 0;
    top: 0;
    
    
}
.modal-dialog {
    margin: auto;
    position: relative;
    display: table-cell;
    border: 1px #777 solid;
    background-color: #f3f3f3;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    animation-name: example;
    animation-duration: 1.5s;
    text-align: center;

/*     padding: 0;
    outline: 0;
 */}
.container {
    padding: 2px 16px;
}
.modal:target {
    display: table;
    /*  position: absolute;  */
}
.closebtn {
    text-decoration: none;
    float: right;
    font-size: 25px;
    font-weight: bold;
    margin: 10px;
}
.closebtn:hover,
.closebtn:focus {
    color: #777;
    cursor: pointer;
}

</style>