---
Created: Invalid date
Updated: Invalid date
---
mongoose

elegant mongodb object modeling for node.js

writing MongoDB validation, casting and business logic boilerplate is a drag

Mongoose provides a straight-forward, schema-based solution to model your application data.

It includes built-in type casting, validation, query building, business logic hooks and more, out of the box.

// schema**var** kittySchema = mongoose.Schema({  
    name: String  
});  
kittySchema.methods.speak = **function** () {  
  **var** greeting = **this**.name  
    ? "Meow name is " + **this**.name  
    : "I don't have a name";  
  
  console.**log**(greeting);}**var** Kitten = mongoose.model('Kitten', kittySchema);