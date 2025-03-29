<script setup>
import { ref } from "vue";

defineProps({
  msg: String,
});

const name = ref("");
const fullName = ref("");
const number = ref("");
const email = ref("");

// مقدار اولیه برای نمایش تمام مخاطبین
const activeDisplay = ref("all");

// کلاس‌های استایل‌دهی
const classes = {
  "bg-blue-700": true,
  "active:bg-blue-800": true,
  "hover:bg-blue-600": true,
  "py-1": true,
  "rounded-md": true,
  "mx-1": true,
  "cursor-pointer": true,
  "text-white": true,
  "text-center": true,
};

// تابع برای انتخاب کلاس مناسب
const getClass = (type) => {
  return activeDisplay.value === type ? classes : "";
};

// استایل‌های دیگر
const btn = ref(
  "bg-blue-700 active:bg-blue-800 hover:bg-blue-600 text-white w-[370px] my-2 py-1 rounded-md cursor-pointer"
);
const inputs = ref("border border-gray-300 w-[370px] py-1 px-3 rounded-md");
const text = ref("text-center my-3 text-gray-500 font-bold");

// تغییر تب فعال هنگام کلیک روی آیتم‌ها
const setActiveDisplay = (type) => {
  activeDisplay.value = type;
};
</script>

<template>
  <div class="container mx-auto" style="direction: rtl; max-width: 400px">
    <!-- تب‌های بالای صفحه -->
    <ul class="grid grid-cols-3 mt-20 mb-2">
      <li
        :class="getClass('all')"
        @click="setActiveDisplay('all')"
        class="text-center"
      >
        نمایش همه
      </li>
      <li
        :class="getClass('search')"
        @click="setActiveDisplay('search')"
        class="text-center"
      >
        جستجو
      </li>
      <li
        :class="getClass('add')"
        @click="setActiveDisplay('add')"
        class="text-center"
      >
        افزودن مخاطب
      </li>
    </ul>

    <div
      class="border rounded-xl border-gray-300 shadow-2xl shadow-gray-500 bg-white"
    >
      <!-- بخش نمایش همه -->
      <div v-show="activeDisplay === 'all'">
        <h1 :class="text">نمایش همه</h1>

        <div class="bg-blue-100 m-4 px-3 rounded-md py-1 text-end">
          <span class="px-1">NameAdd </span>
          <span class="text-blue-700 font-bold">{{ name }}</span>
          <hr class="border-blue-400" />
          <span class="px-1">Name </span>
          <span class="text-blue-700 font-bold">{{ fullName }}</span>
          <hr class="border-blue-400" />
          <span class="px-1">Phone </span>
          <span class="text-blue-700 font-bold">{{ number }}</span>
          <hr class="border-blue-400" />
          <span class="px-1">Email </span>
          <span class="text-blue-700 font-bold">{{ email }}</span>
        </div>
      </div>

      <!-- بخش جستجو -->
      <div v-show="activeDisplay === 'search'">
        <h1 :class="text">جستجو مخاطبین</h1>
        <div class="mx-auto text-center my-5">
          <input
            v-model="name"
            type="text"
            placeholder="نام مخاطب را وارد کنید"
            :class="inputs"
          />
          <button :class="btn">جستجو</button>
        </div>
        <div class="bg-blue-100 m-4 px-3 rounded-md py-1 text-end">
          Name
          <span class="text-blue-700 font-bold">{{ name }}</span>
        </div>
      </div>

      <!-- بخش افزودن مخاطب -->
      <div v-show="activeDisplay === 'add'" class="mx-auto my-9 w-[370px]">
        <h1 :class="text">افزودن مخاطب</h1>
        <div class="grid grid-cols-2">
          <div>
            <label class="text-gray-500"
              >نام و نام خانوادگی <span class="text-red-500">:</span></label
            >
            <input
              v-model="fullName"
              type="text"
              class="border border-gray-400 py-1 rounded-md"
              placeholder="متین حسن پور"
            />
          </div>
          <div>
            <label class="text-gray-500"
              >شماره تماس <span class="text-red-500">:</span></label
            >
            <input
              v-model="number"
              type="text"
              class="border border-gray-400 py-1 rounded-md"
              placeholder="*********09"
            />
          </div>
        </div>
        <div>
          <label class="text-gray-500"
            >ایمیل <span class="text-red-500">:</span></label
          >
          <input
            v-model="email"
            type="text"
            :class="inputs"
            placeholder="mattinhasanpour01@gmail.com"
          />
        </div>
        <button :class="btn">ثبت مخاطب</button>
        <div class="bg-blue-100 m-4 px-3 rounded-md py-1 text-end">
          <span class="px-1">Name </span>
          <span class="text-blue-700 font-bold">{{ fullName }}</span>
          <hr class="border-blue-400" />
          <span class="px-1">Phone </span>
          <span class="text-blue-700 font-bold">{{ number }}</span>
          <hr class="border-blue-400" />
          <span class="px-1">Email </span>
          <span class="text-blue-700 font-bold">{{ email }}</span>
        </div>
      </div>
    </div>
  </div>
</template>
