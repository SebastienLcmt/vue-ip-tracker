<template>
    <div class="fit-content position-absolute z-index-result top-100 start-50  translate-middle d-flex flex-column flex-sm-row bg-f1 rounded px-4 px-sm-5 py-2 py-sm-5">
        <div class="d-flex flex-column flex-shrink-0 mx-2 mx-sm-3 mx-md-4 align-items-center ">
            <h3 class="fs-6 fw-lighter mb-1 mb-sm-2">IP Address</h3>
            <span class="fs-6"> {{ ipData.address }} </span>
        </div>
        <div class="d-flex flex-column flex-shrink-0 mx-2 mx-sm-3 mx-md-4 align-items-center">
            <h3 class="fs-6 fw-lighter mb-1 mb-sm-2 ">Location</h3>
            <span class="fs-6"> {{ipData.city}} </span>
        </div>
        <div class="d-flex flex-column flex-shrink-0 mx-2 mx-sm-3 mx-md-4 align-items-center">
            <h3 class="fs-6 fw-lighter mb-1 mb-sm-2">Timezone</h3>
            <span class="fs-6">UTC {{ipData.timezone}}</span>
        </div>
        <div class="d-flex flex-column flex-shrink-0 mx-2 mx-sm-3 mx-md-4 align-items-center">
            <h3 class="fs-6 fw-lighter mb-1 mb-sm-2">Isp</h3>
            <span class="fs-6">{{ipData.isp}}</span>
        </div>
    </div>

</template>

<script>
    export default {
        name: 'IPinfo',
        props: ['ipData']

    }
</script>
