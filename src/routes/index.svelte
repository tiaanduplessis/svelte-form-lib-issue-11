<script lang='typescript'>
  import Textfield from '@smui/textfield'
  import {createForm} from 'svelte-forms-lib';
  import * as yup from 'yup'
  import HelperText from '@smui/textfield/helper-text/index';

  const {
    form, errors, state, touched, isValid, isSubmitting,
    isValidating, handleBlur, handleChange, handleSubmit
  } = createForm({
    initialValues: {
      title: '',
      name: '',
      email: ''
    },
    validationSchema: yup.object().shape({
      name: yup.string().required(),
      email: yup.string().email().required()
    }),

    onSubmit: values => {
      alert(JSON.stringify(values));
    }
  });

</script>

<form class:valid = {$isValid}
      on:submit = {handleSubmit}>

  <div>
    <Textfield id = 'email'
               name = 'email'
               type = 'email'
               label = 'Email'
               on:change = {handleChange}
               bind:value = {$form.email}/>    {#if $errors.email && $touched.email}
    <HelperText validationMsg>{$errors.email}</HelperText>    {/if}  </div>
  <div>{$errors.email}</div>
</form>