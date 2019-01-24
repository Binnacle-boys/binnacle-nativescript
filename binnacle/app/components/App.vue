<template>
    <Page class="page">
        <ActionBar class="action-bar" style="background: #777">
            <Label class="action-bar-title" text="Accelerometer Vue Demo"></Label>
        </ActionBar>

        <ScrollView>
            <StackLayout class="home-panel">
                <StackLayout>
                    <Button text="Start Accelerometer" @tap="startAccelerometer"
                        :visibility="accelerometerValues.x ? 'collapsed' : 'visible'" />
                    <StackLayout :visibility="accelerometerValues.x ? 'visible' : 'collapsed'">
                        <Label :text="'X: ' + accelerometerValues.x" />
                        <Label :text="'Y: ' + accelerometerValues.y" />
                        <Label :text="'Z: ' + accelerometerValues.z" />
                    </StackLayout>
                </StackLayout>
        </StackLayout>
    </ScrollView>
    </Page>
</template>

<script>
    const accelerometer = require("nativescript-accelerometer");
    let accelerometerListening = false;

    export default {
        methods: {
            startAccelerometer: function() {
                if (accelerometerListening) {
                    accelerometer.stopAccelerometerUpdates();
                }
                accelerometer.startAccelerometerUpdates(
                    data => {
                        accelerometerListening = true;
                        this.accelerometerValues = data;
                    }, {
                        sensorDelay: "ui"
                    }
                );
            }
        },

        data() {
            return {
                accelerometerValues: {
                    x: null,
                    y: null,
                    z: null
                }
            };
        }
    };
</script>

<style scoped lang="scss">

</style>