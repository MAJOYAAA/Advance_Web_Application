<script setup>
import { ref } from 'vue';

const brgy = ref ('')

</script>


<template>

<div class="container mt-3">
  <h3>Hello Sir</h3>
  <p>Click to know our Barangay</p>
  
  <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#myModal">
    Open
  </button>
</div>


<div class="modal" id="myModal">
  <div class="modal-dialog">
    <div class="modal-content">

      <!-- Modal Header -->
      <div class="modal-header">
        <h4 class="modal-title">Please choose</h4>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>

      <!-- Modal body -->
      <div class="modal-body">
        <select v-model="brgy">
            <option value="" disabled>choose from options</option>
            <option value="1">San Isidro</option>
            <option value="2">Otavi</option>
            <option value="3">Quezon</option>
            <option value="4">Aguinaldo</option>
        </select>

        <p v-if="brgy == '1'">Mary Joy Godala</p>
        <p v-else-if="brgy == '2'">Maricel Carciller</p>
        <p v-else-if="brgy == '3'">Jamel Mahusay</p>
        <p v-else-if="brgy == '4'">Jinky Hatap</p>

      </div>

      <!-- Modal footer -->
      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Close</button>
      </div>

    </div>
  </div>
</div>

</template>