<template>
    <div>
        <div class="row mt-4">
            <div class="col-lg-12">
                <div class="breadcrumb-main user-member justify-content-sm-between ">
                    <div class=" d-flex flex-wrap justify-content-center breadcrumb-main__wrapper">
                        <div class="d-flex align-items-center user-member__title justify-content-center mr-sm-25">
                            <h4 class="text-capitalize fw-500 breadcrumb-title">Employee</h4>
                            <span class="sub-title ml-sm-25 pl-sm-25">{{employeeCount}} Employees</span>
                        </div>
                    </div>
                    <div class="action-btn">
                        <router-link to="/employee/new" class="btn btn-sm btn-primary-boxity btn-add">
                            <em class="las la-plus fs-16"></em>New employee</router-link>
                    </div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-lg-12">
                <div class="userDatatable global-shadow border p-15 bg-white radius-xl w-100 mb-30">
                    <div class="table-responsive">
                        <v-card-title>
                            <v-text-field v-model="search" append-icon="mdi-magnify" label="Search here..." single-line
                                hide-details></v-text-field>
                        </v-card-title>
                        <v-data-table :loading="loading" :search="search" loading-text="Loading... Please wait"
                            :headers="headers" :items="employeeData" :items-per-page="10" class="elevation-1">
                            <template v-slot:[`item.employee_sex`]="{ item }">
                                <div v-if="item.employee_sex==true">
                                    <span><i class="far fa-mars"></i> Male</span>
                                </div>
                                <div v-if="item.employee_sex==false">
                                    <span><i class="far fa-venus"></i> Female</span>
                                </div>
                            </template>
                            <template v-slot:[`item.status`]="{ item }">
                                <span class="rounded-pill userDatatable-content-status color-success
                                            bg-opacity-success text-capitalize" v-if="item.status ==1"> Active</span>
                                <span class="rounded-pill userDatatable-content-status color-danger
                                            bg-opacity-danger text-capitalize" v-if="item.status ==0"> Resigned</span>
                                <span class="rounded-pill userDatatable-content-status color-danger
                                            bg-opacity-danger text-capitalize" v-if="item.status ==2"> Not
                                    Active</span>
                            </template>
                            <template v-slot:[`item.actions`]="{item}">
                                <router-link :to="`/employee/detail/${item.id}`" class="edit">
                                    <i class="fad fa-eye"></i></router-link>
                            </template>
                        </v-data-table>
                    </div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col-xxl-12 col-lg-12 col-md-12 mb-25">
                <div class="feature-cards5 d-flex justify-content-between border-0 radius-xl bg-white p-25">
                    <div class="application-task d-flex align-items-center">
                        <div class="application-task-content">
                            <span><strong>Need help?</strong> Check out our <a href="https://help.boxity.id"
                                    target="_blank">documentation</a> or our <a href="#">getting
                                    started video series</a> to quickly learn the basics or <router-link
                                    to="/new-issue">reach out to our
                                    team</router-link>, we'd happy to help.</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        title() {
            return 'Employee';
        },
        data() {
            return {
                // datatable
                search: '',
                employeeData: [],
                key: 1,
                loading: true,
                headers: [{
                    text: 'Employee Code',
                    value: 'employee_code'
                }, {
                    text: 'Full Name',
                    value: 'employee_name'
                }, {
                    text: 'Sex',
                    value: 'employee_sex'
                }, {
                    text: 'Department',
                    value: 'department.departments_name'
                }, {
                    text: 'Sub Department',
                    value: 'subdepartment.subdepartments_name'
                }, {
                    text: 'Join Date',
                    value: 'date_join'
                }, {
                    text: 'Status',
                    value: 'status'
                }, {
                    text: 'Action',
                    align: 'center',
                    value: 'actions'
                }],
                // end datatable
            }
        },
        computed: {
            employeeCount() {
                return this.employeeData.length
            }
        },
        created() {
            this.loadEmployee();
        },
        methods: {
            async loadEmployee() {
                // this.$Progress.start();
                this.$isLoading(true);
                const resp = await axios.get('/api/employee');
                if (resp.data.length) {
                    this.loading = false;
                }
                this.employeeData = resp.data;
                // this.$Progress.finish();
                this.$isLoading(false);
            },
        },
    }

</script>
