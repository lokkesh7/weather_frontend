<template>
    <div class="highlights-item col-md-4 col-sm-6 col-xs-12 border-left border-right border-top">
        <div>
            <div class="card-heading pt-5">Visibility</div>
            <div class="row pt-4 mt-4">
                <div class="col-sm-12 col-md-12 mt-2 text-center align-middle">
                    <p class="card-sub-heading mt-3">Air Visibility</p>
                    <p class="mt-4"><img src="../assets/winddirection.svg" height="40" width="40"></p>
                    <p class="card-value mt-4">{{ airVisibility }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { toRefs } from 'vue'
export default {
    props: ['visibility'],
    setup (props) {
        const {visibility} = toRefs(props)
        return {airVisibility: visibility}
    }
}
</script>

<style lang="scss" scoped>

</style>