<style>
    #app {
      /*border: black dashed 1px;*/
      width: 1100px;
      padding: 0 20px 20px 60px;
      flex: content;
    }
    #app > table{
      width: 1020px;
      /*height: 30px;
      background-color: lightcoral;
      padding: 20px;*/
      align-items: center;
    }

   table thead{
      width: 1020px;
      height: 30px;
      background-color: lightcoral;
      /*padding: 20px;*/
      align-items: center;
    }

    #app h1 {
      font-weight: bold;
      font-family: 'Courier New', Courier, monospace;
      font-size: large;
    }

    #create {
      background-color:darkcyan;
      color: white;
      border-radius: 5px;
      box-shadow: 2px;
      transition: all;
    }
  </style>

<template>
    <div id="app">
    <h1>
      My Inertia CRUD
    </h1>
    <Link
      id="create"
      href="posts/create">
      Create new Post
    </Link>
    <table>
      <thead>
        <tr>
          <th v-for="header in headers" :key="header">
            {{ header }}
          </th>
        </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts" :key="post.id">
            <td>{{ post.title }}</td>
            <td>{{ post.body }}</td>
            <td>
                <button @click="deletePost(post.id)">Delete</button>
                <Link :href="`posts/${post.id}/edit`">Edit</Link>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { Link, useForm } from "@inertiajs/vue3";
  defineProps({
    posts: {
      type: Array,
      default: () => [],
    },
  });
  
  const headers = ["title", "body", "actions"];

  const form = useForm({});

  const deletePost = (id) => {
        form.delete(`posts/${id}`);
    };
  </script>