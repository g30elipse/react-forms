- [react-form](#react-form)
	- [Installation](#installation)
	- [Getting started with react-forms](#getting-started-with-react-forms)
	- [Built In Components](#built-in-components)
	- [Configuration File](#configuration-file)
	- [Sampe Object Structures](#sampe-object-structures)
	- [Setting default props](#setting-default-props)
	- [Add your own Component](#add-your-own-component)
	- [Adding Condition to your form field.](#adding-condition-to-your-form-field)
	- [Validating Form Fields](#validating-form-fields)
	- [Initial Values](#initial-values)
	- [Managing Form action](#managing-form-action)

# react-form

Hi! This is a react library that builds a form component for you.
It uses basic [material-ui](https://www.npmjs.com/package/@material-ui/core) library for designing and [formik](https://www.npmjs.com/package/formik) library for form action handling. 

## Installation

    npm i react-forms

## Getting started with react-forms

    import {ReactForm} from 'react-forms'
    import React from 'react'

    export default const MyReactComponent = () => {
    const myConfig = [{
    type : 'text',
    valueKey : 'myTextField',
    fieldProps : { label : 'Sample Text Field' , fullWidth: true } ,
    } ]
    const myInitialValues = [{ myTextField : '' }]
    return ( <div>
    <ReactForm
    config={myConfig}
    initialValues={myInitialValue}
    onSubmit = {(values : object) => {console.log(values)}}  
	/></div> )
	}

## Built In Components

 - Text Field
 - Autocomplete
 - Check box
 - Radio button
 - Select Field
 - Switch
 - Place Suggest Field
 - Date / Time Picker

## Configuration File

 ***Type :***
The config file is a an array , where each item is an Object or array of Object.
Each item represents a row , so if the item contains single object then there will be single component in the row or else the form width will be distributed among the column components.
***Object Structure :***
*type* : string (component you want to render)
*valueKey* : string  (unique key used to identify the field)
*fieldProps*: Accept all the default props available in their respective material-ui Api
*styles*: CSS style object to be applied on the wrapper. Each component is wrapped around with a div component.

*You don't need to pass any onChange since it all will be handled by the form builder using formik library*

## Sampe Object Structures 

 1. **TextField** :    

        {
        type : 'text',
        valueKey: 'myText'
        fieldProps : { ...textFieldProps }
        styles : { margin : '0 auto'}
        }
	textFieldProps = [TextFieldProps](https://material-ui.com/api/text-field/)

   

  2. **SelectField** :

	

    {
    	type : 'select'
    	valueKey: 'mySelect'
    	fieldProps : {
    		...selectProps
    		options :[{name : 'Abc' , value : 'abc'} , {name : 'XYZ' , value : 'xyz'}] 
    			}
    		styles : { width : '50%' }
    }

selectProps = [SelectProps](https://material-ui.com/api/select/)

 3. **Checkbox**

        { 
	    type : 'checkbox'
	    valueKey: 'myCheckbox',
	    fieldProps : { 
		    ...checkboxProps , 
		    options :[{name : 'Abc' , value : 'abc'} , {name : 'XYZ' , value : 'xyz'}] ,
		    header : 'My Checkbox Header',
		    formControlLabelProps : formcontrollabelprops,
		    formcontrolProps : formcontrolprops
		    formHelperTextProps : formhelpertextprops
		    }
	    }
    ***Options** can be an Array of string or Array of {name , value} object. This structure is followed by SelectField , Checkbox and Radiobutton.*

 **Except options all other props are optional and**

    formControlLabelProps : [formcontrollabelprops](https://material-ui.com/api/form-control-label/#formcontrollabel-api),

   formcontrolProps : [formcontrolprops](https://material-ui.com/api/form-control/#formcontrol-api)
   formHelperTextProps : [formhelpertextprops](https://material-ui.com/api/form-helper-text/#formhelpertext-api)
  checkboxProps : [CheckboxProps](https://material-ui.com/api/checkbox/)

 4. **Radio Button**

	    {
	    type : 'radio' ,
	    valueKey : 'myRadio' ,
		    fieldProps : {
				...radioProps ,
				options :[{name : 'Abc' , value : 'abc'} , {name : 'XYZ' , value : 'xyz'}],
				formcontrolProps : formcontrolprops
			        formHelperTextProps : formhelpertextprops
		}
	    }
	radioProps : [RadioButtonProps](https://material-ui.com/api/radio/)

 5. **Switch** 
 

	    {
	    type : 'switch' , 
	    valueKey : 'mySwitch',
	    fieldProps : { label : 'Demo Switch'
			    ...switchProps
			  }
	    }
	switchProps = [SwitchProps](https://material-ui.com/api/switch/)

6. **Password**

	

	    {
		    type : 'password' ,
		    valueKey : 'myPassswordField'		  
		    fieldProps :{
				label : 'Enter password',
				...textFieldProps
			}
	    }

7. **File :**

$mdFormatter$11$mdFormatter$

``` 
	{
		type: 'file',
		valueKey: 'myfile',
		fieldProps:{
			readAs?: 'readAsBinaryString' | 'readAsDataURL' | 'readAsArrayBuffer' | 'readAsText'
			encoding?: string
			disabled?: boolean
			multiple?: boolean
			accept?: string
			disableDefaultTooltip?: boolean
			invisible?: boolean
			onFilesChange?: (files: FileList) => void
			onDone?: (imgFiles: TFile[], remFiles?: File[]) => void
			wrapWith?: (input: JSX.Element) => JSX.Element
			nativeInputProps?: React.InputHTMLAttributes<{}>
		}
	}
	```

	**Notes :**

  + Do not specify encoding if readAs is not set to readAsText. It will throw an error since only text can have encoding  property in JS' FileReader.
  + Any props specified in nativeInputProps will override other defaults and properties set in the component. 
  + Function passed to wrapWith should take the input Element and return the same within the wrapped element. The input element is always invisible if wrapWith is provided
  + Specify the type of files you want to accept using accept.

  

## Setting default props

You can set your own default props for a specific field that would be used all over the application. All you need to do is use the setDefaultProps() method and pass the field type and your default props object.
**Example :**

    import {setDefaultProps} from 'react-forms'
	setDefaultProps('text' , {fullWidth : true , color : 'secondary'})

Now this props would be default properties followed throughout the application.
And of course if you don't want to use them somewhere then you can pass your own fieldProps in config file.

## Add your own Component

If you want to create your own custom component then we have provided a attachField property for you.

    import {react , FC} from 'react'
    import  {attachField} from 'react-forms'
    const YourComponent:FC<> = () =>{
		return <div/>
		}
	attachField('your-component',<YourComponent/> ,{default-props})

## Adding Condition to your form field.

Just imagine if you want to make a component behave differently based on the state of another component. Well it is possible by passing condition props to the config file. 
*Check this example on sandbox*

    const config = [{
			type : 'text' ,
			valueKey : 'myText'
		},{
			type " text',
			valueKey : 'myText2'
		},{
			type : 'radio' ,
			valueKey : 'myRadio',
			fieldProps :{
				options : ['option1' , 'option2']
			},
			condition : {
				hidden : true ,
				defaultProps : { same as fieldProps} ,
				truthyProps : { same as fieldProps} ,
				logicOpn : 'AND' | 'OR',
				values : [{
					key : 'myText',
					compareValue : 30 ,
					operator : '==='
				},{
					key : 'myText2',
					compareValue : 'abc ,
					operator : '!=='
				}
				]
			}
		}]

 ***Note:***

	 

 - hidden : if True the component  will be rendered if and only if the given conditions are true.
 - logicOpn : AND or OR
 - defaultProps : this props will be passed with fieldprops if the necessary conditions are not satisfied.
 - truthyProps : this props will be passed with fieldProps if the conditions are satisfied.
 - values : every object in the array contains a 

		 - key : which uniquely identifies the field in the form.
		 - compareValue : the value to be compared with the value of the field identified by the key.
		 - operator : comparition operator.

## Validating Form Fields 

No form is complete without some some constraints or validation.
We use [YUP](https://www.npmjs.com/package/yup) library for all kind of field validations.
example : 

	

    import * as YUP from 'yup'
    import { ReactForm } from 'react-forms'
    const formValidation = Yup.object({
	    offerType: Yup.string().required('Select atleast 1 offer'),
	    myText: Yup.number().max(50)
	    })
	const config = [{
		type : 'text',
		value : 'myText'
	},
	{
	    type: 'radio',
	    valueKey: 'offerType',
	    fieldProps: {
	    options: [{
		    name: 'Offer1',
		    value: 1
		    }, {
		    name: 'Offer2',
		    value: 2
		    }],
	    header: 'My Offers',
	    }}]
	   export default const Example:FC <> =() =>{
		return <div>
				<ReactForm
					config = {config}
					validationSchema = {formValidation}
					onSubmit={(values:object)=>{console.log(values)} />
			</div>
		}

Once you hit the submit button it will perform validation as per the validation schema.

## Initial Values 

You can provide initial values if you want to the field of your choice.
All you need to do is pass an array that looks something like this:

	[ {valueKey : value} , {valueKey : value} .....]

    initVals = [ {myText : 'Init Value' , myCheckBox : ['option_2'] }

## Managing Form action

Now the form is filled , what to do next?
Well the last thing which the ReactForm takes is an actionConfig object.
*The Structure*

    actionConfig = {
	    submitButtonText : string,
	    submitButtonLayout : 'right'|'center'|'fullwidth'
	    submitButtonProps : submitbuttonprops,
	    loaderProps : loaderprops,
	    actionContent : Custom JSX Component
    }
    

  [submitbuttonprops](https://material-ui.com/api/button/)
[loaderprops](https://material-ui.com/api/circular-progress/#circularprogress-api)

Dependencies

1. formik
2. lodash
3. @material-ui/core
4. @material-ui/icons
