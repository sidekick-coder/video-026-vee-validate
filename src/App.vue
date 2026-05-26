<script setup>
import { useForm, Field } from 'vee-validate';
import { toTypedSchema } from '@vee-validate/valibot'
import * as v from 'valibot'
import AddressField from './AddressField.vue';
import { ref } from 'vue';

const schema = v.object({
  name: v.pipe(v.string(), v.minLength(3)),
  email: v.pipe(v.string(), v.email()),
  age: v.number(),
  gender: v.picklist(['male', 'female']),
  address: v.object({
    city: v.string(),
    state: v.string(),
    address: v.string(),
    number: v.number(),
  })
})

const result = ref()

const { handleSubmit, errors } = useForm({
  validationSchema: toTypedSchema(schema)
})

const onSubmit = handleSubmit((data) => {
  result.value = data
})

</script>
<template>
  <div class="flex h-screen items-center justify-center">
    <form @submit="onSubmit" class="flex flex-col gap-y-4 border p-4 rounded border-zinc-500 w-full max-w-md">
      <h1 class="font-bold">Sign up</h1>
      <Field type="text" name="name" />
      <Field type="text" name="email" />
      <Field type="number" name="age" />
      <Field name="gender" as="select">
        <option value="male">Male</option>
        <option value="female">Female</option>
      </Field>

      <AddressField name="address" />

      <button type="submit">Submit</button>

      <div>
        <div v-for="(e, key) of errors" class="text-red-500">
          {{key}}: {{  e }}
        </div>
      </div>
    </form>

    <div v-if="result" class="fixed inset-0 bg-black/80 flex items-center justify-center" @click="result = null">
      <pre class="bg-white rounded p-4">{{ result }}</pre>
    </div>
  </div>
</template>
