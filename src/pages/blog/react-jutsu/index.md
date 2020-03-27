---
title: 'jutsu'
date: '2020-03-27'
image: 'https://source.unsplash.com/150x150/?remote+work'
excerpt: A jitsi meet component wrapper moulded with react's chakra
---

<p align="center">
    <img src="https://source.unsplash.com/600x300/?remote+work"/>
    <i style="color: var(--dark-color-lighter)">random image from unsplash</i>
</p>

I have been reading a bit about WebRTC and how those video conferencing apps work given the situation we're all in due COVID-19

One project that caught my attention recently was [jitsi](https://jitsi.org/)

They're open source and quite nice to work with, in their api [docs](https://github.com/jitsi/jitsi-meet/blob/master/doc/api.md) they go over how to embed jitsi in your application

I decided to use that in a React project I am currently working on and made that into a shared component since I didn't find anything out there

You can see a live demo using the public jitsi domain [here](https://this-fifo.github.io/jutsu/)

## How to use it

```bash
yarn add react-jutsu
```

## Add the Jitsi Meet API js file to the html body

```html
<body>
  <script src='https://meet.jit.si/external_api.js'></script>
</body>
```

## Sample Usage

```jsx
import React, { useState } from 'react'

import Jutsu from 'react-jutsu'

const App = () => {
  const [room, setRoom] = useState('')
  const [name, setName] = useState('')
  const [call, setCall] = useState(false)

  const handleClick = event => {
    event.preventDefault()
    if (room && name) setCall(true)
  }

  return call ? (
    <Jutsu
      roomName={room}
      userName={name}
      loadingComponent={<p>loading ...</p>} />
  ) : (
    <form>
      <input id='room' type='text' placeholder='Room' value={room} onChange={(e) => setRoom(e.target.value)} />
      <input id='name' type='text' placeholder='Name' value={name} onChange={(e) => setName(e.target.value)} />
      <button onClick={handleClick} type='submit'>
        Start / Join
      </button>
    </form>
  )
}

export default App
```

## Supported Configuration
> Check the [Jitsi Meet API docs](https://github.com/jitsi/jitsi-meet/blob/master/doc/api.md#api--new-jitsimeetexternalapidomain-options) for more

### Room Name
The meeting room name
>This prop is required for jitsi to load

### User Name
The participant's name
>This prop is required for jitsi to load

### Domain
```jsx
<Jutsu domain='my-custom-domain.com'>
```
Your Jitsi domain to use, the default value is `meet.jit.si`

### Loading Component
```jsx
<Jutsu loadingComponent={<ProgressBar />}>
```
An optional loading component, the default value is `<p>Loading ...</p>`

### Styles
```jsx
<div
  style={{...containerStyle, ...containerStyles}}
>
  <div
    style={{...jitsiContainerStyle, ...jitsiContainerStyles}}
  />
</div>
```
Internally Jutsu is constructed inside 2 containers, you can add custom styles for each by specifying `containerStyles` and `jitsiContainerstyles`

The default values are

```js
const containerStyle = {
  width: '800px',
  height: '400px'
}

const jitsiContainerStyle = {
  display: loading ? 'none' : 'block', // <- used for loadingComponent logic
  width: '100%',
  height: '100%'
}
```

An example override could be
```jsx
<Jutsu containerStyles={{ width: '1200px', height: '800px' }}>
```

Feel free to grab it out for your next project or help me modify it to suit your needs, the code is open source and you can find it [here](https://github.com/this-fifo/jutsu)
