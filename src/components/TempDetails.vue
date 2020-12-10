<template>
    <div class="custom-card header-card card">
        <div class="card-body pt-0">
            <div class="row first-row">
                <div class="col-lg-6 title">
                    Minimum Temperature
                    <div class="subtitle">
                        {{temp.minTemp}}
                    </div>
                </div>
                <div class="col-lg-6 title ">
                    Maximum Temperature
                    <div class="subtitle">
                        {{temp.maxTemp}}
                    </div>
                </div>
            </div>
            <div class="row second-row">
                <div class="col-lg-6 title">
                    Feels Like
                    <div class="subtitle">
                        {{temp.feelsLike}}
                    </div>
                </div>
                <div class="col-lg-6 title">
                    Pressure
                    <div class="subtitle">
                        {{temp.pressure}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { toRefs } from 'vue'
export default {
    props: ['tempDetails'],
    setup (props) {
        const {tempDetails} = toRefs(props)

        return {temp: tempDetails}
    }
}
</script>

<style scoped>
    .first-row {
        margin-top: 60px;
    }
    .second-row {
        margin-top: 80px;
    }
    .title {
        font-size: 40px;
    }
    .subtitle {
        font-size: 24px;
    }
</style>