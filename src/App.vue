<script setup>
import { RouterLink, RouterView } from 'vue-router';

const users = [
    {
      "id":"0052v00000bX0m1AAC",
      "name":"Admin",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000hbBjFAAU",
      "name":"Integration User",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000b0kB9AAK",
      "name":"Security User",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000bX0m0AAP",
      "name":"Platform Integration User",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000hbdhlAAA",
      "name":"Chatter Expert",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"Chatter Free User",
      "password":"admin@123"
    },
    {
      "id":"0052v00000bX0m1AAA",
      "name":"Automated Process",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000hbBjFAAF",
      "name":"Integration User",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000b0kB9AAI",
      "name":"Security User",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000bX0m0AAC",
      "name":"Platform Integration User",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"System Admin",
      "password":"admin@123"
    },
    {
      "id":"0052v00000hbdhlAAJ",
      "name":"Chatter Expert",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"Chatter Free User",
      "password":"admin@123"
    },
    {
      "id":"0052v00000hbdhlAAD",
      "name":"Dev I",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"IT Manager",
      "password":"admin@123"
    },
    {
      "id":"0052v00000hbdhlAAV",
      "name":"Dev II",
      "email":"AutomatedProcess@yopmail.com",
      "phone":"0123456789",
      "role":"IT Manager",
      "password":"admin@123"
    },
];

localStorage.setItem('user', JSON.stringify(users));
</script>

<template>
  <RouterView />
</template>
