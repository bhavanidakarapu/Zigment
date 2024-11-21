# Zigment
import React from 'react'; import { useForm, SubmitHandler } from 'react-hook-form'; const FormRenderer = ({ schema }: { schema: any }) => { const { register, handleSubmit, formState: { errors } } = useForm(); const onSubmit: SubmitHandler<any> = (data) => { console.log(data); alert('Form submitted successfully!'); }; return ( <form onSubmit={handleSubmit(onSubmit)} className="p-4"> <h1 className="text-xl font-bold mb-2">{schema.formTitle}</h1> <p className="mb-4">{schema.formDescription}</p> {schema.fields.map((field: any) => ( <div key={field.id} className="mb-4"> <label className="block mb-1">{field.label}</label> {field.type === 'text' field.type === 'email' ? ( <input {...register(field.id, { required: field.required })} placeholder={field.placeholder} type={field.type} className="border rounded p-2 w-full" /> ) : field.type === 'select' ? ( <select {...register(field.id, { required: field.required })} className="border rounded p-2 w-full" > {field.options.map((option: any) => ( <option key={option.value} value={option.value}> {option.label} </option> ))} </select> ) : null} {errors[field.id] && ( <span className="text-red-500">{field.validation?.message 'This field is required.'}</span> )} </div> ))} <button type="submit" className="bg-blue-500 text-white px-4 py-2 rounded">Submit</button> </form> ); }; export default FormRenderer; 
json
Copy code
{ "formTitle": "Project Requirements Survey", "formDescription": "Please fill out this survey about your project needs", "fields": [ { "id": "name", "type": "text", "label": "Full Name", "required": true, "placeholder": "Enter your full name" }, ... ] } 
Tests
Run unit tests:
bash
Copy code
npm run test 
Run end-to-end tests:
bash
Copy code
npx playwright test 
Deployment
Deployed on Vercel
