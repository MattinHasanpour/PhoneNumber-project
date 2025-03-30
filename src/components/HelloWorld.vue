<script setup>
import { ref } from "vue";

const contact = ref([]); // آرایه خالی بدون آیتم اولیه

const searchName = ref("");
const fullName = ref("");
const phoneNumber = ref("");
const emailAddress = ref("");
const activeDisplay = ref("all");

// تعریف متغیر text
const text = ref("text-center my-3 text-gray-500 font-bold");

// کلاس‌های استایل‌دهی
const activeClass = {
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

const inactiveClass = {
  "py-1": true,
  "mx-1": true,
  "cursor-pointer": true,
  "text-center": true,
};

// استایل‌های دیگر
const btn =
  "bg-blue-700 active:bg-blue-800 hover:bg-blue-600 text-white w-[370px] my-2 py-1 rounded-md cursor-pointer";
const inputs = "border border-gray-300 w-[370px] py-1 px-3 rounded-md";

// تابع برای انتخاب کلاس مناسب
const getClass = (type) => {
  return activeDisplay.value === type ? activeClass : inactiveClass;
};

// تابع برای اضافه کردن مخاطب جدید
const addContact = () => {
  if (fullName.value && phoneNumber.value && emailAddress.value) {
    contact.value.push({
      name: fullName.value,
      phone: phoneNumber.value,
      email: emailAddress.value,
    });
    fullName.value = "";
    phoneNumber.value = "";
    emailAddress.value = "";
  }
  $.toaster({
    message: "اطلاعات شما به سایت اضافه شد",
    title: "موقیت آمیز",
    priority: "success",
  });
  $.toaster("اطلاعات شما به سایت اضافه شد", "موقیت آمیز", "success");
};
</script>

<template>
  <div class="container mx-auto" style="direction: rtl; max-width: 400px">
    <!-- تب‌های بالای صفحه -->
    <ul class="grid grid-cols-3 mt-20 mb-2">
      <li :class="getClass('all')" @click="activeDisplay = 'all'">نمایش همه</li>
      <li :class="getClass('search')" @click="activeDisplay = 'search'">
        جستجو
      </li>
      <li :class="getClass('add')" @click="activeDisplay = 'add'">
        افزودن مخاطب
      </li>
    </ul>

    <div
      class="border rounded-xl border-gray-300 shadow-2xl shadow-gray-500 bg-white"
    >
      <!-- بخش نمایش همه -->
      <div v-show="activeDisplay === 'all'">
        <h1 :class="text">نمایش همه</h1>
        <ul>
          <li
            class="bg-red-100 text-red-600 py-3 text-center my-6 mx-3 rounded-sm"
            v-if="contact.length === 0"
          >
            Not Contact ❌
          </li>
          <template v-else>
            <li
              class="px-4 border-b border-gray-200 hover:rounded-2xl hover:bg-gray-50 cursor-pointer"
              v-for="(item, index) in contact"
              :key="index"
            >
              <p class="grid grid-cols-2 py-3">
                <span class="text-center"> 📞 {{ item.phone || "---" }} </span>
                <span class="text-center"> 👤 {{ item.name || "---" }} </span>
              </p>
              <p class="py-3 text-center">📪 {{ item.email || "---" }}</p>
            </li>
          </template>
        </ul>
      </div>

      <!-- بخش جستجو -->
      <div v-show="activeDisplay === 'search'">
        <h1 :class="text">جستجو مخاطبین</h1>
        <div class="mx-auto text-center my-5">
          <input
            v-model="searchName"
            type="text"
            placeholder="نام مخاطب را وارد کنید"
            :class="inputs"
          />
          <button :class="btn">جستجو</button>
        </div>
        <div
          v-if="searchName"
          class="bg-blue-100 m-4 px-3 rounded-md py-1 text-end"
        >
          نام جستجو شده:
          <span class="text-blue-700 font-bold">{{ searchName }}</span>
        </div>
      </div>

      <!-- بخش افزودن مخاطب -->
      <div v-show="activeDisplay === 'add'">
        <h1 :class="text">افزودن مخاطب</h1>
        <div class="mx-auto my-5 w-[370px]">
          <div class="grid grid-cols-2 gap-4 mb-4">
            <div>
              <label class="text-gray-500 block mb-1">
                نام و نام خانوادگی <span class="text-red-500">*</span>
              </label>
              <input
                v-model="fullName"
                type="text"
                class="border border-gray-400 w-full py-1 px-2 rounded-md"
                placeholder="متین حسن پور"
                required
              />
            </div>
            <div>
              <label class="text-gray-500 block mb-1">
                شماره تماس <span class="text-red-500">*</span>
              </label>
              <input
                v-model="phoneNumber"
                minlength="11"
                maxlength="11"
                type="tel"
                class="border border-gray-400 w-full py-1 px-2 rounded-md"
                placeholder="*********09"
                required
              />
            </div>
          </div>
          <div class="mb-4">
            <label class="text-gray-500 block mb-1">
              ایمیل <span class="text-red-500">*</span>
            </label>
            <input
              v-model="emailAddress"
              type="email"
              class="border border-gray-400 w-full py-1 px-2 rounded-md"
              placeholder="mattinhasanpour01@gmail.com"
              required
            />
          </div>
          <button
            :class="btn"
            @click="addContact"
            :disabled="!fullName || !phoneNumber || !emailAddress"
          >
            ثبت مخاطب
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
