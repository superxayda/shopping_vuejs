<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import {computed} from "vue";
import {useStore} from "vuex";
import config from "./config";
import axios from "axios";
import {ref} from "vue";

const store = useStore();
const email = ref("")
const password = ref("")
const userStatus = computed(() => {
  return store.state.userStatus;
});
//const userStatus = ref("")
const activeTab = computed(() => {
  return store.state.activeTab;
});

//const activeTab = ref("shop");

const changeTab = (tab: string) => {
  store.commit("chgActiveTab", tab);
};

// const query_token = "http://" + config.apiServer + ":" + config.port + "/api/current_user";
// axios.get(query_token,{headers:{'Authorization':"Bearer " + localStorage.getItem('Authorization')}}).then((res) => {
//   console.log(res.data);
//   store.commit('chgUser', {
//       accId: res.data.uuid,
//       userEmail: res.data.email,
//       userName: res.data.email.split('@')[0]}
//       // userName: res.data.type }
//   )
//   // alert(res.data.uuid)
//   if (res.data.type === 'vendor') {
//     userStatus: 'vendor'
//     store.commit('chgStatus', 'vendor')
//   } else {
//     userStatus: 'active'
//     store.commit('chgStatus', 'active')
//   }
// });
</script>

<template>
  <div class="mb-24">
    <router-view class=""/>
  </div>
  <div class="w-full my-5">
    <div
        class="inline-block text-center mx-auto fixed inset-x-0 bottom-0 z-10 bg-white border-t-1 shadow-2xl p-3"
    >
      <div class=" justify-center flex space-x-4" id="nav">
        <router-link
            v-if="userStatus !== 'vendor'"
            to="/"
            class="rounded-lg px-5 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900"
            :class="{ active: activeTab === '' }"
            @click="changeTab('')"
        >
          <svg
              v-if="activeTab !== ''"
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M8.9375 21.8809H19.2734C20.9697 21.8809 21.9541 20.8965 21.9541 19.0156V9.91895C21.9541 8.03809 20.9609 7.05371 19.0625 7.05371H17.8232C17.7793 5.08496 16.1006 3.4502 14 3.4502C11.9082 3.4502 10.2207 5.08496 10.1768 7.05371H8.9375C7.03906 7.05371 6.0459 8.03809 6.0459 9.91895V19.0156C6.0459 20.8965 7.03906 21.8809 8.9375 21.8809ZM14 5.00586C15.2041 5.00586 16.0918 5.91113 16.127 7.05371H11.873C11.9082 5.91113 12.7959 5.00586 14 5.00586ZM9.05176 20.1318C8.24316 20.1318 7.79492 19.71 7.79492 18.8574V10.0771C7.79492 9.2334 8.24316 8.81152 9.05176 8.81152H18.9482C19.748 8.81152 20.2051 9.2334 20.2051 10.0771V18.8574C20.2051 19.71 19.748 20.1318 19.1592 20.1318H9.05176Z"
                fill="#1C1C1E"
            />
          </svg>
          <svg
              v-else
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M8.9375 21.8809H19.2734C20.9697 21.8809 21.9541 20.8965 21.9541 19.0156V9.91895C21.9541 8.03809 20.9609 7.05371 19.0625 7.05371H17.8232C17.7793 5.08496 16.1006 3.4502 14 3.4502C11.9082 3.4502 10.2207 5.08496 10.1768 7.05371H8.9375C7.03906 7.05371 6.0459 8.03809 6.0459 9.91895V19.0156C6.0459 20.8965 7.03906 21.8809 8.9375 21.8809ZM14 5.00586C15.2041 5.00586 16.0918 5.91113 16.127 7.05371H11.873C11.9082 5.91113 12.7959 5.00586 14 5.00586Z"
                fill="#1C1C1E"
            />
          </svg>
          <div v-if="activeTab !== ''" class="text-xs text-gray-500 text-center">
            Store
          </div>
          <div v-else class="text-xs text-gray-800 text-center">Store</div>
        </router-link>
        <router-link
            v-if="userStatus !== 'visitor'"
            to="/profile"
            class="rounded-lg px-5 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900"
            :class="{ active: activeTab === 'profile' }"
            @click="changeTab('profile')"
        >
          <svg
              v-if="activeTab !== 'profile'"
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M14 13.8477C16.127 13.8477 17.8496 11.9668 17.8496 9.66406C17.8496 7.39648 16.127 5.59473 14 5.59473C11.8818 5.59473 10.1416 7.42285 10.1504 9.68164C10.1592 11.9756 11.873 13.8477 14 13.8477ZM14 12.3096C12.7871 12.3096 11.7588 11.1582 11.7588 9.68164C11.75 8.24023 12.7783 7.13281 14 7.13281C15.2305 7.13281 16.2412 8.22266 16.2412 9.66406C16.2412 11.1406 15.2217 12.3096 14 12.3096ZM8.51562 22.0215H19.4756C20.9961 22.0215 21.7256 21.5381 21.7256 20.501C21.7256 18.084 18.7109 14.8672 14 14.8672C9.28906 14.8672 6.26562 18.084 6.26562 20.501C6.26562 21.5381 6.99512 22.0215 8.51562 22.0215ZM8.24316 20.4834C8.03223 20.4834 7.95312 20.4131 7.95312 20.2549C7.95312 18.9102 10.124 16.4053 14 16.4053C17.8672 16.4053 20.0381 18.9102 20.0381 20.2549C20.0381 20.4131 19.959 20.4834 19.748 20.4834H8.24316Z"
                fill="#1C1C1E"
            />
          </svg>
          <svg
              v-else
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M14.0088 13.5752C15.9248 13.5752 17.5508 11.8701 17.5508 9.66406C17.5508 7.51074 15.916 5.8584 14.0088 5.8584C12.0928 5.8584 10.4492 7.53711 10.458 9.68164C10.458 11.8701 12.084 13.5752 14.0088 13.5752ZM8.52441 21.749H19.4756C20.9258 21.749 21.4268 21.3096 21.4268 20.501C21.4268 18.2422 18.5615 15.1309 14 15.1309C9.44727 15.1309 6.57324 18.2422 6.57324 20.501C6.57324 21.3096 7.07422 21.749 8.52441 21.749Z"
                fill="#1C1C1E"
            />
          </svg>
          <div v-if="activeTab !== 'profile'" class="text-xs text-gray-500 text-center">
            My
          </div>
          <div v-else class="text-xs text-gray-800 text-center">My</div>
        </router-link>
        <router-link
            v-if="userStatus === 'visitor'"
            to="/login"
            class="rounded-lg px-5 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900"
            :class="{ active: activeTab === 'login' }"
            @click="changeTab('login')"
        >
          <svg
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M14 22.7422C18.9834 22.7422 23.0879 18.6289 23.0879 13.6543C23.0879 8.67969 18.9658 4.56641 13.9912 4.56641C9.36816 4.56641 5.50098 8.1084 4.98242 12.5996C5.52734 12.4766 6.24805 12.4414 6.82812 12.5381C7.34668 9.04004 10.335 6.38574 13.9912 6.38574C18.0254 6.38574 21.2773 9.62012 21.2773 13.6543C21.2773 15.5791 20.5391 17.3193 19.3174 18.6113C18.4121 17.6094 16.4961 16.6953 13.9912 16.6953C13.209 16.6953 12.4795 16.7832 11.8203 16.9414C11.9258 17.3633 11.9785 17.8027 11.9785 18.251C11.9785 19.6836 11.4248 21.0107 10.5283 22.0391C11.6006 22.4873 12.7783 22.7422 14 22.7422ZM13.9912 15.2539C15.6963 15.2627 17.0234 13.8125 17.0234 11.9316C17.0234 10.1562 15.6875 8.6709 13.9912 8.6709C12.3037 8.6709 10.9502 10.1562 10.9678 11.9316C10.9766 13.8125 12.2861 15.2363 13.9912 15.2539ZM6.19531 22.7861C8.65625 22.7861 10.7217 20.7295 10.7217 18.251C10.7217 15.7725 8.68262 13.7246 6.19531 13.7246C3.7168 13.7246 1.66895 15.7725 1.66895 18.251C1.66895 20.7383 3.7168 22.7861 6.19531 22.7861ZM3.32129 18.251C3.32129 17.8906 3.56738 17.6533 3.92773 17.6533H5.58887V15.9922C5.58887 15.6318 5.82617 15.3857 6.19531 15.3857C6.56445 15.3857 6.80176 15.6318 6.80176 15.9922V17.6533H8.46289C8.82324 17.6533 9.06934 17.8906 9.06934 18.251C9.06934 18.6201 8.82324 18.8574 8.46289 18.8574H6.80176V20.5273C6.80176 20.8877 6.56445 21.1338 6.19531 21.1338C5.82617 21.1338 5.58887 20.8877 5.58887 20.5273V18.8574H3.92773C3.56738 18.8574 3.33008 18.6201 3.32129 18.251Z"
                fill="#1C1C1E"
            />
          </svg>
          <div v-if="activeTab !== 'login'" class="text-xs text-gray-500 text-center">
            Login
          </div>
          <div v-else class="text-xs text-gray-800 text-center">Login</div>
        </router-link>
        <router-link
            v-if="userStatus !== 'vendor' && userStatus !== 'visitor'"
            to="/cart"
            class="rounded-lg px-5 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900"
            :class="{ active: activeTab === 'cart' }"
            @click="changeTab('cart')"
        >
          <svg
              v-if="activeTab !== 'cart'"
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M10.7393 18.6553H20.9697C21.3828 18.6553 21.7607 18.3301 21.7607 17.8643C21.7607 17.4072 21.3828 17.082 20.9697 17.082H10.9414C10.5195 17.082 10.2559 16.792 10.1943 16.3438L10.0625 15.4297H21.04C22.3848 15.4297 23.0967 14.6123 23.29 13.2764L23.9492 8.87305C23.9668 8.75879 23.9844 8.60938 23.9844 8.5127C23.9844 7.99414 23.624 7.64258 23.0176 7.64258H8.92871L8.79688 6.69336C8.68262 5.92871 8.375 5.54199 7.39941 5.54199H4.38477C3.94531 5.54199 3.55859 5.92871 3.55859 6.37695C3.55859 6.83398 3.94531 7.2207 4.38477 7.2207H7.13574L8.49805 16.5195C8.69141 17.8467 9.39453 18.6553 10.7393 18.6553ZM22.1562 9.21582L21.6025 13.1182C21.5322 13.5664 21.2949 13.8477 20.8643 13.8477L9.83398 13.8564L9.15723 9.21582H22.1562ZM11.46 23.0674C12.3125 23.0674 12.998 22.3818 12.998 21.5293C12.998 20.6768 12.3125 19.9912 11.46 19.9912C10.6074 19.9912 9.92188 20.6768 9.92188 21.5293C9.92188 22.3818 10.6074 23.0674 11.46 23.0674ZM19.5811 23.0674C20.4336 23.0674 21.1104 22.3818 21.1104 21.5293C21.1104 20.6768 20.4336 19.9912 19.5811 19.9912C18.7285 19.9912 18.0342 20.6768 18.0342 21.5293C18.0342 22.3818 18.7285 23.0674 19.5811 23.0674Z"
                fill="#1C1C1E"
            />
          </svg>
          <svg
              v-else
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M3.55859 6.37695C3.55859 6.83398 3.94531 7.2207 4.38477 7.2207H7.13574L8.49805 16.5195C8.69141 17.8467 9.39453 18.6553 10.7393 18.6553H20.9697C21.3828 18.6553 21.7607 18.3301 21.7607 17.8643C21.7607 17.4072 21.3828 17.082 20.9697 17.082H10.9414C10.5195 17.082 10.2559 16.792 10.1943 16.3438L10.0537 15.4297H21.04C22.3848 15.4297 23.0967 14.6123 23.29 13.2764L23.9492 8.87305C23.9668 8.75879 23.9844 8.60938 23.9844 8.5127C23.9844 7.99414 23.624 7.64258 23.0176 7.64258H8.9375L8.79688 6.69336C8.68262 5.92871 8.375 5.54199 7.39941 5.54199H4.38477C3.94531 5.54199 3.55859 5.92871 3.55859 6.37695ZM9.92188 21.5293C9.92188 22.3818 10.6074 23.0674 11.46 23.0674C12.3125 23.0674 12.998 22.3818 12.998 21.5293C12.998 20.6768 12.3125 19.9912 11.46 19.9912C10.6074 19.9912 9.92188 20.6768 9.92188 21.5293ZM18.0342 21.5293C18.0342 22.3818 18.7285 23.0674 19.5811 23.0674C20.4336 23.0674 21.1104 22.3818 21.1104 21.5293C21.1104 20.6768 20.4336 19.9912 19.5811 19.9912C18.7285 19.9912 18.0342 20.6768 18.0342 21.5293Z"
                fill="#1C1C1E"
            />
          </svg>
          <div v-if="activeTab !== 'cart' " class="text-xs text-gray-500 text-center">
            Cart
          </div>
          <div v-else class="text-xs text-gray-800 text-center">Cart</div>
        </router-link>
        <router-link
            v-if="userStatus === 'vendor'"
            to="/manage"
            class="shadow-lg border-2 bg-white border-slate-600  rounded-full px-5 py-2 text-slate-700 font-medium"
            :class="{ active: activeTab === 'vendor' }"
            @click="changeTab('vendor')"
        >
          <button v-if="activeTab !== 'vendor'" class="text-white text-lg text-center">
            <svg width="40" height="40" viewBox="0 0 28 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path
                  d="M6.45898 20.29C6.45898 22.1885 7.43457 23.1729 9.31543 23.1729H18.6758C20.5566 23.1729 21.5322 22.1885 21.5322 20.29V7.02734C21.5322 5.1377 20.5566 4.14453 18.6758 4.14453H9.31543C7.43457 4.14453 6.45898 5.1377 6.45898 7.02734V20.29ZM8.18164 20.1846V7.13281C8.18164 6.31543 8.60352 5.86719 9.45605 5.86719H18.5264C19.3789 5.86719 19.8096 6.31543 19.8096 7.13281V20.1846C19.8096 21.002 19.3789 21.4502 18.5264 21.4502H9.45605C8.60352 21.4502 8.18164 21.002 8.18164 20.1846ZM10.7393 8.91699H17.5332C17.8496 8.91699 18.0957 8.66211 18.0957 8.3457C18.0957 8.03809 17.8496 7.80078 17.5332 7.80078H10.7393C10.4141 7.80078 10.1768 8.03809 10.1768 8.3457C10.1768 8.66211 10.4141 8.91699 10.7393 8.91699ZM10.7393 11.4395H14.7119C15.0371 11.4395 15.2744 11.1846 15.2744 10.8682C15.2744 10.5605 15.0371 10.3232 14.7119 10.3232H10.7393C10.4141 10.3232 10.1768 10.5605 10.1768 10.8682C10.1768 11.1846 10.4141 11.4395 10.7393 11.4395ZM10.8711 19.8506H17.1289C17.8848 19.8506 18.2715 19.4639 18.2715 18.708V13.9795C18.2715 13.2324 17.8848 12.8457 17.1289 12.8457H10.8711C10.1416 12.8457 9.71973 13.2324 9.71973 13.9795V18.708C9.71973 19.4639 10.1416 19.8506 10.8711 19.8506Z"
                  fill="#1C1C1E"/>
            </svg>

          </button>
          <button v-else class="text-white text-lg text-center">
            <svg width="40" height="40" viewBox="0 0 28 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path
                  d="M6.45898 20.29C6.45898 22.1885 7.43457 23.1729 9.31543 23.1729H18.6758C20.5566 23.1729 21.5322 22.1885 21.5322 20.29V7.02734C21.5322 5.1377 20.5566 4.14453 18.6758 4.14453H9.31543C7.43457 4.14453 6.45898 5.1377 6.45898 7.02734V20.29ZM10.6162 8.73242C10.2734 8.73242 10.0273 8.47754 10.0273 8.14355C10.0273 7.81836 10.2734 7.56348 10.6162 7.56348H17.665C17.999 7.56348 18.2451 7.81836 18.2451 8.14355C18.2451 8.47754 17.999 8.73242 17.665 8.73242H10.6162ZM10.6162 11.3516C10.2734 11.3516 10.0273 11.0967 10.0273 10.7627C10.0273 10.4463 10.2734 10.2002 10.6162 10.2002H14.7383C15.0723 10.2002 15.3184 10.4463 15.3184 10.7627C15.3184 11.0967 15.0723 11.3516 14.7383 11.3516H10.6162ZM10.7568 20.0791C10.001 20.0791 9.56152 19.6748 9.56152 18.8926V13.9971C9.56152 13.2148 10.001 12.8193 10.7568 12.8193H17.2432C18.0254 12.8193 18.4297 13.2148 18.4297 13.9971V18.8926C18.4297 19.6748 18.0254 20.0791 17.2432 20.0791H10.7568Z"
                  fill="#1C1C1E"/>
            </svg>

          </button>
        </router-link>
        <router-link
            v-if="userStatus !== 'visitor'"
            to="/order"
            class="rounded-lg px-5 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900"
            :class="{ active: activeTab === 'order' }"
            @click="changeTab('order')"
        >
          <svg
              v-if="activeTab !== 'order'"
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M6.30078 19.2705L13.2617 23.1553C13.7451 23.4277 14.2373 23.4277 14.7207 23.1553L21.6816 19.2705C22.5342 18.7959 22.9561 18.3037 22.9561 17.0645V9.93652C22.9561 9.00488 22.6045 8.41602 21.8135 7.96777L15.6348 4.50488C14.5537 3.89844 13.4375 3.89844 12.3477 4.50488L6.16895 7.96777C5.38672 8.41602 5.03516 9.00488 5.03516 9.93652V17.0645C5.03516 18.3037 5.45703 18.7959 6.30078 19.2705ZM18.1133 10.4463L11.6182 6.81641L13.0596 6.00781C13.6924 5.64746 14.29 5.63867 14.9316 6.00781L20.4688 9.12793L18.1133 10.4463ZM13.9912 12.749L7.52246 9.12793L9.94824 7.74805L16.4346 11.3779L13.9912 12.749ZM7.26758 17.9082C6.78418 17.6357 6.61719 17.3633 6.61719 16.8975V10.5166L13.165 14.208V21.2393L7.26758 17.9082ZM20.7236 17.9082L14.8174 21.2393V14.208L21.3652 10.5166V16.8975C21.3652 17.3633 21.1982 17.6357 20.7236 17.9082Z"
                fill="#1C1C1E"
            />
          </svg>
          <svg
              v-else
              width="28"
              height="28"
              viewBox="0 0 28 28"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="M19.0801 10.2178L22.3408 8.38086C22.2002 8.24023 22.0332 8.12598 21.8135 8.01172L15.6523 4.54883C15.1074 4.24121 14.5449 4.08301 14 4.08301C13.4463 4.08301 12.8838 4.24121 12.3389 4.54883L10.6514 5.49805L19.0801 10.2178ZM13.9912 13.0566L17.7266 10.9648L9.3418 6.23633L6.17773 8.01172C5.9668 8.12598 5.79102 8.24023 5.65039 8.38086L13.9912 13.0566ZM14.6416 23.2959C14.7295 23.2783 14.8086 23.2344 14.8965 23.1904L21.6992 19.376C22.5518 18.8926 22.9912 18.3916 22.9912 17.1348V10.1035C22.9912 9.88379 22.9736 9.69922 22.9297 9.52344L14.6416 14.1992V23.2959ZM13.3496 23.2959V14.1992L5.06152 9.52344C5.01758 9.69922 5 9.88379 5 10.1035V17.1348C5 18.3916 5.43945 18.8926 6.29199 19.376L13.0947 23.1904C13.1738 23.2344 13.2617 23.2783 13.3496 23.2959Z"
                fill="#1C1C1E"
            />
          </svg>
          <div v-if="activeTab !== 'order'" class="text-xs text-gray-500 text-center">
            Order
          </div>
          <div v-else class="text-xs text-gray-800 text-center">Order</div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<style>
.active {
  background-color: #f3f5f9;
}

body {
  background-color: #f3f5f9;
}
</style>
