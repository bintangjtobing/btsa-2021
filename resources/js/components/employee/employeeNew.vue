<template>
    <div>
        <div class="row mt-4">
            <div class="col-lg-12">
                <div class="breadcrumb-main">
                    <h4 class="text-capitalize fw-500 breadcrumb-title">Create new employee data</h4>
                </div>
            </div>
        </div>
        <div class="row">
            <span @click="routerBack" class="btn btn-circle-light-boxity fa-center"><i
                    class="fad fa-arrow-left"></i></span>
            <span @click="routerRefresh" class="btn btn-circle-light-boxity fa-center"><i
                    class="fad fa-sync"></i></span>
        </div>
        <div class="row">
            <div class="col-lg-12">
                <div class="card mb-3">
                    <div class="card-body">
                        <div class="form-row">
                            <div class="col-lg-2">
                                <div class="form-group">
                                    <span>Employee code:</span>
                                    <input v-model="employeeData.employee_code" type="text" class="form-control" />
                                </div>
                            </div>
                            <div class="col-lg-3">
                                <div class="form-group">
                                    <span>Employee name:</span>
                                    <input v-model="employeeData.employee_name" type="text" class="form-control" />
                                </div>
                            </div>
                            <div class="col-lg-2">
                                <div class="form-group">
                                    <span>Nickname:</span>
                                    <input v-model="employeeData.employee_nickname" type="text" class="form-control" />
                                </div>
                            </div>
                            <div class="col-lg-2">
                                <div class="form-group">
                                    <span>Sex:</span>
                                    <select v-model="employeeData.employee_sex"
                                        class="form-control form-control-default ip-gray radius-xs b-light px-15 fa-select"
                                        id="">
                                        <option value="0">Female</option>
                                        <option value="1">Male</option>
                                    </select>
                                </div>
                            </div>
                            <div class="col-lg-1">
                                <div class="form-group">
                                    <span>Age:</span>
                                    <input v-model="employeeData.employee_age" readonly type="text"
                                        class="form-control" />
                                </div>
                            </div>
                            <div class="col-lg-2">
                                <div class="form-group">
                                    <span>Working duration:</span>
                                    <input v-model="employeeData.employee_working_duration" type="text"
                                        class="form-control" readonly />
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-lg-12">
                <div class="user-info-tab w-100 bg-white global-shadow radius-xl mb-50">
                    <div class="ap-tab-wrapper border-bottom ">
                        <ul class="nav px-30 ap-tab-main text-capitalize" id="v-pills-tab" role="tablist"
                            aria-orientation="vertical">
                            <li class="nav-item">
                                <a class="nav-link active" id="v-pills-details-photo-tab" data-toggle="pill"
                                    href="#v-pills-details-photo" role="tab" aria-controls="v-pills-details-photo"
                                    aria-selected="true">Details and Photo</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link" id="v-pills-contact-info-medical-tab" data-toggle="pill"
                                    href="#v-pills-contact-info-medical" role="tab"
                                    aria-controls="v-pills-contact-info-medical" aria-selected="true">Contact Info &
                                    Medical</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link" id="v-pills-advanced-tab" data-toggle="pill"
                                    href="#v-pills-advanced" role="tab" aria-controls="v-pills-advanced"
                                    aria-selected="true">Advanced</a>
                            </li>
                        </ul>
                    </div>
                    <div class="tab-content" id="v-pills-tabContent">
                        <div class="tab-pane fade  show active" id="v-pills-details-photo" role="tabpanel"
                            aria-labelledby="v-pills-details-photo-tab">
                            <div class="row mx-4">
                                <div class="col-lg-12">
                                    <div class="card card-vertical card-default card-md mb-4">
                                        <div class="card-body pb-md-30">
                                            <div class="vertical-form">
                                                <form @submit.prevent="handleSubmit" enctype="multipart/form-data"
                                                    method="POST">
                                                    <h5>Details</h5>
                                                    <div class="form-row">
                                                        <div class="col-lg-2">
                                                            <div class="form-group">
                                                                <span>Birth place:</span>
                                                                <input type="text" v-model="employeeData.birth_place"
                                                                    placeholder="Birth place" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee') ">
                                                            </div>
                                                        </div>
                                                        <div class="col-lg-3">
                                                            <div class="form-group">
                                                                <span>Birth date:</span>
                                                                <input type="date" v-model="employeeData.birth_date"
                                                                    placeholder="Birth date" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee')">
                                                            </div>
                                                        </div>
                                                        <div class="col-lg-3">
                                                            <div class="form-group">
                                                                <span>Join of Date:</span>
                                                                <input type="date" v-model="employeeData.date_join"
                                                                    placeholder="Join of Date" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee')">
                                                            </div>
                                                        </div>
                                                        <!-- <div class="col-lg-4 px-5">
                                                            <div class="account-profile justify-content-center ">
                                                                <div class="ap-img pro_img_wrapper">
                                                                    <input id="file-upload" type="file"
                                                                        name="fileUpload" class="d-none"
                                                                        @change="fileUpload">
                                                                    <label for="file-upload">
                                                                        <img class="ap-img__main rounded-circle wh-120 bg-lighter d-flex"
                                                                            :src="employeeData.employee_pic"
                                                                            v-if="!imagePreview" alt="employee picture">
                                                                        <img class="ap-img__main rounded-circle wh-120 bg-lighter d-flex"
                                                                            :src="imagePreview" alt="profile img"
                                                                            v-if="imagePreview">
                                                                        <span class="cross" id="remove_pro_pic">
                                                                            <i class="fal fa-camera"></i>
                                                                        </span>
                                                                    </label>
                                                                </div>
                                                            </div>
                                                        </div> -->
                                                    </div>
                                                    <div class="form-row">
                                                        <div class="col-lg-3">
                                                            <div class="form-group">
                                                                <span>Nationality:</span>
                                                                <input type="text" v-model="employeeData.nationality"
                                                                    placeholder="Nationality" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee')">
                                                            </div>
                                                        </div>
                                                        <div class="col-lg-9">
                                                            <div class="form-group">
                                                                <span>Identity No:</span>
                                                                <input type="number" v-model="employeeData.identity_no"
                                                                    placeholder="Identity number" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee')">
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="form-row">
                                                        <div class="col-lg-2">
                                                            <div class="form-group">
                                                                <span>Weight:</span>
                                                                <input type="number" v-model="employeeData.weight"
                                                                    placeholder="Weight" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee')">
                                                            </div>
                                                        </div>
                                                        <div class="col-lg-2">
                                                            <div class="form-group">
                                                                <span>Height:</span>
                                                                <input type="number" v-model="employeeData.height"
                                                                    placeholder="Height" class="form-control"
                                                                    :disabled="!permissions.includes('CreateEmployee')">
                                                            </div>
                                                        </div>
                                                        <div class="col-lg-5">
                                                            <div class="form-group">
                                                                <span>Religion:</span>
                                                                <select v-model="employeeData.religion"
                                                                    class="form-control form-control-default ip-gray radius-xs b-light px-15 fa-select"
                                                                    id="">
                                                                    <option value="Islam">Islam</option>
                                                                    <option value="Protestan">Protestan</option>
                                                                    <option value="Katolik">Katolik</option>
                                                                    <option value="Hindu">Hindu</option>
                                                                    <option value="Buddha">Buddha</option>
                                                                    <option value="Konghucu">Konghucu</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                        <div class="col-lg-3">
                                                            <div class="form-group">
                                                                <span>Blood Type:</span>
                                                                <select v-model="employeeData.blood_type"
                                                                    class="form-control form-control-default ip-gray radius-xs b-light px-15 fa-select"
                                                                    id="">
                                                                    <option value="O">O</option>
                                                                    <option value="A">A</option>
                                                                    <option value="B">B</option>
                                                                    <option value="AB">AB</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <hr style="margin-top:10px; margin-bottom:10px;">
                                                    <h5>Misscellaneous</h5>
                                                    <div class="form-group">
                                                        <div class="form-row">
                                                            <div class="col-lg-6">
                                                                <div class="form-group">
                                                                    <span>Tax ID</span>
                                                                    <input type="number" v-model="employeeData.tax_id"
                                                                        class="form-control"
                                                                        :disabled="!permissions.includes('CreateEmployee')">
                                                                </div>
                                                            </div>
                                                            <div class="col-lg-6">
                                                                <div class="form-group">
                                                                    <span>BPJS/Kesehatan</span>
                                                                    <input type="number" v-model="employeeData.bpjskes"
                                                                        class="form-control"
                                                                        :disabled="!permissions.includes('CreateEmployee')">
                                                                </div>
                                                            </div>
                                                            <div class="col-lg-6">
                                                                <div class="form-group">
                                                                    <span>BPJS/Tenaga Kerja</span>
                                                                    <input type="text" v-model="employeeData.bpjstk"
                                                                        class="form-control"
                                                                        :disabled="!permissions.includes('CreateEmployee')">
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="button-group d-flex pt-25"
                                                        v-if="permissions.includes('CreateEmployee')">
                                                        <button type="submit"
                                                            class="btn btn-primary-boxity btn-default btn-squared text-capitalize">Update
                                                        </button>
                                                    </div>
                                                </form>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="tab-pane fade  show" id="v-pills-contact-info-medical" role="tabpanel"
                            aria-labelledby="v-pills-contact-info-medical-tab">
                            <div class="row mx-4">
                                <div class="col-lg-12">
                                    <div class="card card-vertical card-default card-md mb-4">
                                        <div class="card-body pb-md-30">
                                            <div class="vertical-form">
                                                <h5>Contact</h5>
                                                <div class="form-row">
                                                    <div class="col-lg-6">
                                                        <div class="form-group mb-10">
                                                            <span>Phone:</span>
                                                            <input type="number" v-model="employeeData.phone" id=""
                                                                class="form-control">
                                                        </div>
                                                    </div>
                                                    <div class="col-lg-6">
                                                        <div class="form-group mb-10">
                                                            <span>Email:</span>
                                                            <input type="text" v-model="employeeData.email" id=""
                                                                class="form-control">
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                            <div class="button-group d-flex pt-25"
                                                v-if="permissions.includes('CreateEmployee')">
                                                <button @click="handleSubmit"
                                                    class="btn btn-primary-boxity btn-default btn-squared text-capitalize">Update
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="tab-pane fade  show" id="v-pills-advanced" role="tabpanel"
                            aria-labelledby="v-pills-contact-info-medical-tab">
                            <div class="row mx-4">
                                <div class="col-lg-12">
                                    <div class="card card-vertical card-default card-md mb-4">
                                        <div class="card-body pb-md-30">
                                            <div class="vertical-form">
                                                <h5>Job</h5>
                                                <div class="form-row">
                                                    <div class="col-lg-6">
                                                        <div class="form-group mb-10">
                                                            <span>Job type:</span>
                                                            <!-- <input type="text" v-model="employeeData.job_type" id=""
                                                                class="form-control"> -->
                                                            <select v-model="employeeData.job_type"
                                                                class="form-control form-control-default ip-gray radius-xs b-light px-15 fa-select"
                                                                id="">
                                                                <option value="Probation">Probation</option>
                                                                <option value="Internship">Internship</option>
                                                                <option value="Contract">Contract</option>
                                                                <option value="Full-time">Full-time</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    <div class="col-lg-6">
                                                        <div class="form-group mb-10">
                                                            <span>Department:</span>
                                                            <select v-model="employeeData.departments"
                                                                class="form-control form-control-default ip-gray radius-xs b-light px-15 fa-select"
                                                                id="">
                                                                <option v-for="department in departmentOpt"
                                                                    v-bind:key="department.id" :value="department.id">
                                                                    {{department.departments_name}}</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    <div class="col-lg-6">
                                                        <div class="form-group mb-10">
                                                            <span>Job title:</span>
                                                            <input type="text" v-model="employeeData.job_title" id=""
                                                                class="form-control">
                                                        </div>
                                                    </div>
                                                    <div class="col-lg-6">
                                                        <div class="form-group mb-10">
                                                            <span>Sub Department:</span>
                                                            <select v-model="employeeData.sub_departments"
                                                                class="form-control form-control-default ip-gray radius-xs b-light px-15 fa-select"
                                                                id="">
                                                                <option v-for="subdepartment in subDepartmentOpt"
                                                                    v-bind:key="subdepartment.id"
                                                                    :value="subdepartment.id">
                                                                    {{subdepartment.subdepartments_name}}</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                            <div class="button-group d-flex pt-25"
                                                v-if="permissions.includes('CreateEmployee')">
                                                <button @click="handleSubmit"
                                                    class="btn btn-primary-boxity btn-default btn-squared text-capitalize">Update
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import Swal from 'sweetalert2';
    import Editor from '@tinymce/tinymce-vue';
    import vue2Dropzone from 'vue2-dropzone';
    import VueNumeric from 'vue-numeric'
    export default {
        components: {
            'editor': Editor,
            vueDropzone: vue2Dropzone,
            VueNumeric
        },
        title() {
            return `New Employee data`;
        },
        data() {
            return {
                employeeData: {},
                imagePreview: null,
                departmentOpt: {},
                subDepartmentOpt: {},

                permissions: []
            }
        },
        created() {
            this.loadEmployeeData();
        },
        beforeMount() {
            this.permissions = this.$store.getters.getPermissions;
        },
        methods: {
            routerBack() {
                this.$router.go(-1)
            },
            routerRefresh() {
                this.$isLoading(true);
                this.loadEmployeeData();
                this.$isLoading(false);
            },
            fileUpload(e) {
                this.employeeData.employee_pic = e.target.files[0];
                let reader = new FileReader();
                reader.readAsDataURL(this.employeeData.employee_pic)
                reader.onload = e => {
                    this.imagePreview = e.target.result;
                }
            },
            async loadEmployeeData() {
                // this.$Progress.start();
                this.$isLoading(true);
                // const response = await axios.get('/api/employee/' + this.$route.params.id);
                // this.employeeData = response.data;

                // Load data relation
                const resp = await axios.get('/api/department');
                this.departmentOpt = resp.data;
                const respSub = await axios.get('/api/department/sub');
                this.subDepartmentOpt = respSub.data;
                // this.$Progress.finish();
                this.$isLoading(false);
            },
            async handleSubmit() {
                await axios.post('/api/employee', this.employeeData).then(response => {
                    document.getElementById('ding').play();
                    this.$router.push('/employee');
                    Swal.fire({
                        icon: 'success',
                        title: 'Congratulations',
                        text: 'Success create new employee data',
                    });
                    // this.$router.push('/employee/detail/' + this.$route.params.id);
                }).catch(err => {
                    this.routerRefresh();
                    document.getElementById('failding').play();
                    Swal.fire({
                        icon: 'error',
                        title: 'Error',
                        text: err.response.data.message,
                    }).then((result) => {
                        if (result.isConfirmed) {
                            location.reload();
                        }
                    });
                });
            },
        },
    }

</script>
