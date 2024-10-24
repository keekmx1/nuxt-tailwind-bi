<script setup lang="ts">
// Import router
const router = useRouter();
// Import Sweetalert2
const { $swal }: any = useNuxtApp();

// Create variable
const email = ref("");
const password = ref("");

// Create event submit
const handleSubmit = () => {
  // Check if email and password is not empty
  if (!email.value || !password.value) return;

  // Send data to api
  useFetch("http://localhost:5000/api/auth/login", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      email: email.value,
      password: password.value,
    }),
    onResponse({ request, response }) {
      // if _data.status === ok
      if (response._data.status === "ok") {
        $swal.fire({
          // position: "top-end",
          icon: "success",
          title: "Login successfully!",
          text: "Welcome to our website!",
          showConfirmButton: false,
          // timer: 2000,
        });
        // Delay 2s
        setTimeout(() => {
          // close sweet alert
          $swal.close();

          // Open to dashboard
          router.push("/backend/dashboard");
        }, 2000);
        // alert("Login successfully!");
      } else {
        $swal.fire({
          // position: "top-end",
          icon: "error",
          title: "Login failed!",
          text: "Please try again!",
          showConfirmButton: false,
          timer: 2000,
        });
        // alert("Login failed!");
      }
    },
  });
};
// console.log(email.value, password.value);
</script>

<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <img
        class="mx-auto h-10 w-auto"
        src="/images/logo.webp"
        alt="Your Company"
      />
      <h2
        class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-white"
      >
        Sign in to your account
      </h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form class="space-y-6" action="#" method="POST">
        <div>
          <label
            for="email"
            class="block text-sm font-medium leading-6 text-white"
            >Email address</label
          >
          <div class="mt-2">
            <input
              v-model="email"
              id="email"
              name="email"
              type="email"
              autocomplete="email"
              required
              class="block w-full rounded-md border-0 py-1.5 text-white shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label
              for="password"
              class="block text-sm font-medium leading-6 text-white"
              >Password</label
            >
          </div>
          <div class="mt-2">
            <input
              v-model="password"
              id="password"
              name="password"
              type="password"
              autocomplete="current-password"
              required
              class="block w-full rounded-md border-0 py-1.5 text-white shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
          <div class="text-sm">
            <a
              href="#"
              class="font-semibold text-indigo-600 hover:text-indigo-500"
              >Forgot password?</a
            >
          </div>
        </div>

        <div>
          <button
            type="button"
            @click="handleSubmit"
            class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            Sign in
          </button>
        </div>
      </form>

      <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        <NuxtLink
          to="/register"
          class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500"
          >Register free</NuxtLink
        >
      </p>
    </div>
  </div>
</template>

<style scoped></style>
