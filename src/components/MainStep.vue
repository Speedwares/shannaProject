<template>
    <section class="section">
    <div class="container">
        <div class="columns">
            <div class="column is-8 is-offset-2">
                <horizontal-stepper :steps="demoSteps" @completed-step="completeStep"
                                    @active-step="isStepActive" @stepper-finished="alert">                     
                </horizontal-stepper>
            </div>
        </div>
    </div>
</section>
</template>

<script>
    import HorizontalStepper from 'vue-stepper';

    // This components will have the content for each stepper step.
    import StepOne from './StepOne.vue';
    import StepTwo from './StepTwo.vue';
    import StepThree from './StepThree.vue';

    export default {
        components: {
            HorizontalStepper
        },
        data(){
            return {
                demoSteps: [
                    {
                        icon: 'mail',
                        name: 'first',
                        title: '1',
                        component: StepOne,
                        completed: false

                    },
                    {
                        icon: 'mail',
                        name: 'second',
                        title: '2',
                        component: StepTwo,
                        completed: false
                    }, 
                    {
                        icon: 'mail',
                        name: 'third',
                        title: '3',
                        component: StepThree,
                        completed: false
                    }
                ]
            }
        },
        methods: {
            // Executed when @completed-step event is triggered
            completeStep(payload) {
                this.demoSteps.forEach((step) => {
                    if (step.name === payload.name) {
                        step.completed = true;
                    }
                })
            },
            // Executed when @active-step event is triggered
            isStepActive(payload) {
                this.demoSteps.forEach((step) => {
                    if (step.name === payload.name) {
                        if(step.completed === true) {
                            step.completed = false;
                        }
                    }
                })
            },
            // Executed when @stepper-finished event is triggered
            alert(payload) {
                alert('end')
            }
        }
    }
</script>