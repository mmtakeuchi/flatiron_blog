---
layout: post
title:      "React Forms"
date:       2020-10-19 19:46:16 +0000
permalink:  react_forms
---


Coming into React, a big change to the setup of forms is the input values and submitting the data. In React, most forms will use controlled inputs, where the value is taken from the state. Another step in controlling our form, is to have the ability to update our state.

```
class Form extends React.Component {
  state = {
    firstName: "",
    lastName: ""
  }
 
  render() {
    return (
      <form>
        <input type="text" name="firstName" value={this.state.firstName} />
        <input type="text" name="lastName" value={this.state.lastName} />
      </form>
    )
  }
}
```

Starting from the inital steps of creating our form, we have initialized state with an object. And have firstName and lastName as keys set to an empty string. Moving down to our form, we have the name attribute set to each key in state. And then we have a value attribtue set to the state for each key. The next step is updating our state as we are typing into our inputs. To do this, we can setup a new function to handle the change in inputs that would also update our state for the keys. 

```
handleFirstNameChange = event => {
    this.setState({
      firstName: event.target.value
    })
  }
 
  handleLastNameChange = event => {
    this.setState({
      lastName: event.target.value
    })
  }
```

So starting with our new functions, we can create one for each of our keys, and pass in an event. And inside the function, we call this.setState(). Inside of this function, we will pass in an object for the key with the new value we want. So for instance the handleFirstNameChange() gets the firstName key set to event.target.value, which is being taken from the value of the inputs. Now in order for these to work, we implement them into our forms inputs. 

```
<form>
        <input type="text" onChange={event => this.handleFirstNameChange(event)} value={this.state.firstName} />
        <input type="text" onChange={event => this.handleLastNameChange(event)} value={this.state.lastName} /></form>
```

So we have added and onChange into the inputs with the event parameter, and passing in the handleChange callbacks. These will be called upon each time the input values change. So as we type in new values for each input, we are setting the state to correspond to the new values we are typing. So after setting up our form, all we need to do is submit the form. To start of submitting our form, we begin with another event, onSubmit, and another function to handle the onSubmit event.

```
handleSubmit = event => {
  event.preventDefault()
  let formData = { firstName: this.state.firstName, lastName: this.state.lastName }
  this.sendFormData(formData)
}

<form onSubmit={event => this.handleSubmit(event)}>
      <input type="text" onChange={event => this.handleFirstNameChange(event)} value={this.state.firstName} />
      <input type="text" onChange={event => this.handleLastNameChange(event)} value={this.state.lastName} />
			<input type="submit"/>
    </form>
```

Beginning from the form, we have added the onSubmit event inside the form tag, and passed in a function called, handleSubmit(event). This will be called when we submit our form. The handleSubmit function right above the form describes the process to occur. First we will call event.preventDefault() to stop the form from submitting when its not called. Second is creating a new variable where we are setting the state to the new values from the onChange events. Lastly, is a function to send our new data to another function or page to be used to display our new information. So one way we can do that, is by changing our page a little bit and adding another function to display the information on this page for this example. 

```
state = {
    firstName: "John",
    lastName: "Henry",
    submittedData: []
  }
	
	...
	
handleSubmit = event => {
    event.preventDefault()
    let formData = { firstName: this.state.firstName, lastName: this.state.lastName }
    let dataArray = this.state.submittedData.concat(formData)
    this.setState({submittedData: dataArray})
  }
 
  listOfSubmissions = () => {
    return this.state.submittedData.map(data => {
      return <div><span>{data.firstName}</span> <span>{data.lastName}</span></div>
    })
  }
	
	...
	</form>
        {this.listOfSubmissions()}
      </div>
```

So starting at the top, we have added a new key, submittedData with the value of an array. When we submit our form, we have the new variable dataArray that will add the formData with the state of the submittedData. Then we updated the state of submittedData to equal the new value from dataArray. Then lastly, we use this new data to create the function, listOfSubmissions. We will map through the data from the submittedData array, and return a new div, with the values of the firstName and lastName. At the bottom of our render, right after our form, we will pass in the listOfSubmissions function to display our new div.

This is the basics of our controlled forms work within React. For this example we used two input elements, but we could also use textarea, select, and option that will have a similar structure like this. And if we wanted to use a checkbox or radio button, we could use this similar structure, but change the value to be checked instead. The aspects of using onChange and onSubmit however will be same for all these elements in a form.
