<template>
    <div id="app">
        <h1 class="text-center mt-2">Customized Forms</h1>
        <p class="text-center">Presented by <strong>Member360</strong></p>

        <div class="col-md-12">
<!--            <button class="btn btn-success mr-2" @click="setData">Create New Document Form</button> -->
<!--            <button class="btn btn-success mr-2" @click="createBlank">Create Blank Form</button> -->
            
            <button class="btn btn-info mr-2" @click="getData">Save Form</button>

<!--            <button class="btn btn-info mr-2" @click="viewRenderer">-->
<!--                <span v-show="isRenderer">-->
<!--                    Back to Builder-->
<!--                </span>-->
<!--                <span v-show="!isRenderer">-->
<!--                    View Renderer Form from Basic Configuration-->
<!--                </span>-->
<!--            </button> -->
        </div>

        <hr>

        <FormBuilder v-if="!isRenderer" :schema="schema" v-model="formData"></FormBuilder>

        <div class="row" v-if="isRenderer" style="padding: 20px; margin-right: 0">
            <div class="col-md-12 mb-4">
                <button class="btn btn-success  mr-2" @click="isShowData = !isShowData">
                    <span v-show="isShowData">Hide Form Data</span>
                    <span v-show="!isShowData">Show Form Data</span>
                </button>

                <button class="btn btn-info mr-2" @click="setRandomData">Set Random Data</button>
            </div>

            <FormRenderer :class="{'col-md-9': isShowData, 'col-md-12': !isShowData}"
                          :form-configuration="formData"
                          v-model="formInputData" 
                          :options="options"/>

            <div class="p-0" :class="{'col-md-3': isShowData, 'd-none': !isShowData}">
                <h4>Form Input Data</h4>
                <pre class="code"><code class="code" v-html="JSON.stringify(formInputData, null, 2)"></code></pre>
            </div>
        </div>
    </div>
</template>

<script>
    
    import FormBuilder from "@/components/FormBuilder";
    import FormRenderer from "@/components/FormRenderer";
    import {DEMO_FORM_DATA} from "@/demo-form-data";

    export default {
        components: {
            FormBuilder,
            FormRenderer
        },
        data: () => ({
            formData: null,
            isShowDevNote: false,
            isRenderer: false,
            formInputData: null,
            isShowData: false,
            schema: []
        }),
        methods: {
            getData() {
              // console.log(JSON.stringify(this.formData))
              console.log(JSON.stringify(this.formData.sections))
              console.log(JSON.stringify(this.formData.controls))
            },

            // createBlank() {
            //     this.formData = Object.assign({})
            // },

            // setData() {
            //     this.formData = Object.assign({}, DEMO_FORM_DATA);
            // },

            // viewRenderer() {
            //     if (!this.isRenderer) {
            //         this.setData();
            //         this.isRenderer = true;
            //         return;
            //     }
            //
            //     this.isRenderer = false;
            // },

            // setRandomData() {
            //     const faker = require('faker');
            //
            //     this.$set(this, 'formInputData', {
            //         "name": faker.name.findName(),
            //         "brief-description": faker.company.companyName(),
            //         "long-description": faker.lorem.paragraphs(),
            //         "user_email": faker.internet.email(),
            //         "is_deletable": faker.random.number({min: 0, max:1}),
            //         "doc_props": [""+faker.random.number({min: 1, max:3})],
            //         "doc_date": faker.date.past(),
            //         "doc-process-range": {
            //             startDate: faker.date.past(),
            //             endDate: faker.date.future(),
            //         },
            //         "total_value": faker.finance.amount()
            //     });
            // },
        }
    }
</script>

<style scoped>
    pre {
        background: #333;
        white-space: pre;
        word-wrap: break-word;
        overflow: auto;
    }

    pre.code {
        margin: 20px 0;
        border-radius: 4px;
        border: 1px solid #292929;
        position: relative;
    }

    pre.code code {
        display: block;
        padding: 15px 16px 14px;
        border-left: 1px solid #555;
        overflow-x: auto;
        font-size: 13px;
        line-height: 19px;
        color: #ddd;
    }
</style>
