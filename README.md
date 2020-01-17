# Rect native formly documenation 


### About

Rn-formly is a light-weight React Native implemenation of formly component. 

Basically using rn-formly, you can easily create beautiful forms, signup screens, settings (upcoming in v2) in less than 2 minutes by just passing a JSON. 

RN-formly  supports plugging in custom validators, loading data asynchronously, passing custom errors and includes progress bar to show progress, loadder handles safe area and almost all the popular component you would require to build beautiful area

For Advance user, rn-formly allows you to cuztomise styling of individual componenet as well (see component props below for more information)


### Screenshots 
 <img src="https://user-images.githubusercontent.com/32276134/72256135-7e162f00-362e-11ea-9500-45b552e27660.png" width=250 height=400> <img src="https://user-images.githubusercontent.com/32276134/72256136-7e162f00-362e-11ea-96ff-6da347fae333.png" width=250 height=400>
<img src="https://user-images.githubusercontent.com/32276134/72256137-7e162f00-362e-11ea-971f-bab0288d8955.png" width=250 height=400>
<img src="https://user-images.githubusercontent.com/32276134/72256138-7e162f00-362e-11ea-91e7-1cb2c325c736.png" width=250 height=400> <img src="https://user-images.githubusercontent.com/32276134/72256139-7eaec580-362e-11ea-89cc-80ed6fa3fe5e.png" width=250 height=400>
<img src="https://user-images.githubusercontent.com/32276134/72256141-7eaec580-362e-11ea-9805-7945e5c52d70.png" width=250 height=400>


<img src="https://user-images.githubusercontent.com/32276134/72256142-7eaec580-362e-11ea-9738-efe7ce49e8a4.png" width=250 height=400> <img src="https://user-images.githubusercontent.com/32276134/72256143-7f475c00-362e-11ea-9074-932075147bcc.png" width=250 height=400>
<img src="https://user-images.githubusercontent.com/32276134/72256143-7f475c00-362e-11ea-9074-932075147bcc.png" width=250 height=400>

## Installation 


RN-Formly use following as peerDependency 
1. react-native-device-info
2. react-native-image-crop-picker


```
npm i react-native-device-info --save
npm i rn-formly  --save
```

And if you intend to use image Components then install `react-native-image-crop-picker`

```
npm i react-native-image-crop-picker --save
```

For iOS, If you are using **React Native => 0.60** then simple do 

```
pod install 
```


else follow this [guide](https://github.com/react-native-community/react-native-device-info)


### Setting up image crop picker

#### IOS setup


Image Crop picker requires you to have relavent permission to access camera and storage for both iOS and Android 

1. Go to info.plist and this 

```
<plist version="1.0">
  <dict>
    ...
    <key>NSPhotoLibraryUsageDescription</key>
    <string>$(PRODUCT_NAME) would like access to your photo gallery</string>
    <key>NSCameraUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to use your camera</string>
    <key>NSPhotoLibraryAddUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to save photos to your photo gallery</string>
    <key>NSMicrophoneUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to use your microphone (for videos)</string>
  </dict>
</plist>
```

You refer to following [documentation](https://github.com/react-native-community/react-native-image-picker/blob/master/docs/Install.md)

or look into this [commit](https://github.com/irohitb/formly-example/commit/2814782d01f6f111208089ff4628c28752919d8d)



#### Android Setup 

Add following lines in your android/app/src/main/AndroidManifest.xml

```
 <uses-permission android:name="android.permission.INTERNET" />
 <uses-permission android:name="android.permission.CAMERA" />
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

look at this [commit](https://github.com/irohitb/formly-example/commit/939b81a90c088ed141b12af9ee8fc7340068f106)

If this does not work, refer to following instructions 

1. [For Image Croper](https://github.com/react-native-community/react-native-image-picker/blob/master/docs/Install.md)
2. [For React Native Device Info](https://github.com/react-native-community/react-native-device-info)


## Usage 

To get started/or a try it out, you can clone or checkout the following [repo](https://github.com/irohitb/formly-example)

**Minimilistic Setup Example** 

```
import SignupFormComponent from 'rn-formly';


const inputFields = [
  {
    key: 'name', 
    type: 'text', 
    label: `Your Full Name`,
    required: true,
    helper: 'Using your real name would make it more likely for you to get a match',
    templateOptions: { 
      componentProps: {
        placeholder: 'Frank Murphy'
      }
    }
  }, 
  {
    key: 'otp', 
    type: 'otp', 
    label: 'Enter OTP',
    helper: '(optional) but try to enter incorrect date', 
    templateOptions: {
      noOfTextInput: 5,
    }
  }]
  
  const App: () => React$Node = () => {

  const justLogDataFromForms = (index, key, currentValue,  payload) => {
     console.log('Logging from Parent log')
    console.log(index, key, currentValue, payload)
  }

  return (
    <>
      <SignupFormComponent 
      inputFields={inputFields}
      globalButtonText={'Next'}
      onButtonClick={justLogDataFromForms}
      defaultColor={'green'}
      ProgressBarProps={{
        blink: false
      }}
      /> 
    </>
  );
};

```

### Required Props 

| **SNO** | **Prop** | **Type** | **Default** | **Required** | **description** | 
|----------|----------|-------------|--------------|-------------|----------|
| 1. | inputFields | Array | Nope | Yes | Click here to know more |
| 2. | onButtonClick | function | Nope | Yes | Passed function recives `index` of the element in array, `key` associated with it and the complete payload till now |

### Optional Props

Important Props are highlighted

#### General Optional Props 

| **SNO** | **Prop** | **Type** | **Default** | **Required** | **description** | 
|----------|----------|-------------|--------------|-------------|----------|
| 1. | textStyle | stylesheet object | none | No | Heading text style (style for your `label` key in `inputFields` props) | 
| 2. | ProgressBar | object | blink: false | No | click here to know more about ProgressBar Component | 
| 3. | helperTextStyle | stylesheet object | none | No | Helper text style (style for your `helper` key in `inputFields` )
| 4. |  backgroundViewColor | string | 'white' | No | background for the view of your form | 
| **5.** | **defaultColor** | **string**  | **'black'** | **no** | **Formats button color, text color and sub component color accordingly (can be override by passing styles for individual component)** | 
| **6.** | **onFinish** | **function** | **none** | **No** | **Function which is triggered after user have itterated over all the elements in the passed inputFields** |
| 7. | backIconStyle | stylesheet object | none | No | Styling for the back button `<` | 

#### Button Optional props 

Validation and Error throwing are done in `inputFields` array. See `inputFields` section to know more

| **SNO** | **Prop** | **Type** | **Default** | **Required** | **description** | 
|----------|----------|-------------|--------------|-------------|----------|
| 1. | buttonSelectedStyle | stylesheet object | none | No | Styling of the button when user is allowed to move to the next field |
| 2. | buttonNotSelectedStyle | stylesheet object | none | No | Styling of the button when user is not allowed to move to the next field |
| 3. | buttonSelectedTextStyle | stylesheet object | none | No | styling of the text inside the button when user is allowed to move to the next field | 
| 4. | buttonNotSelectedTextStyle | stylesheet object | none | no | styling of the text inside the button when user is not allowed to move to the next field |

#### Error Props 

Validation and Error throwing are done in `inputFields` array. See `inputFeilds` section to know more

| **SNO** | **Prop** | **Type** | **Default** | **Required** | **description** | 
|----------|----------|-------------|--------------|-------------|----------|
| 1. | defaultErrorMessage | string | 'Sorry Something went wrong' | No | Error message for user when error occurs but the error does not contain a message for failure |
| 2. | errorStyle | stylesheet object | none | No | Text Styling for error message | 




