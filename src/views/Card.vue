<script>
    export default {
        props: ['value','visible','position','matched'],
        setup(props,context) {
             /* const visible=false
            return {
                visible
            } */
            const selectCard=() => {
                context.emit('select-card',{
                    position: props.position,
                    faceValue: props.value
                
                })
            }
            return {
                selectCard

            }
        }

    }
</script>
<template>
    <div class="card" @click="selectCard" >
        <div v-if="visible" class="card-face is-front">
            {{value}} - {{position}}  - {{matched}}

        </div>
        <div v-else class="card-face is-back">
            Back
        </div>
    </div>

</template>

<style scoped>

    .card {
        border: 5px solid #ccc;
        position: relative;
    }
    .card-face {
        width: 100%;
        height: 100%;
        position: absolute;
    }
    .card-face.is-front {
        background-color: red;
        color: white;
    }
    .card-face.is-back {
        background-color: blue;
        color: white;
    }

</style>