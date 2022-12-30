class ClockExtension {
  constructor () {
    // code for initializing the extension goes here
  }

  getInfo () {
    return {
      id: 'clock',
      name: 'Clock Extension',
      blocks: [
        {
          opcode: 'getTime',
          blockType: BlockType.REPORTER,
          text: 'current time in GMT'
        }
      ]
    }
  }

  getTime () {
    // code for getting the current time from the world clock at https://greenwichmeantime.com/timepiece/world-clock/ goes here
    return new Promise((resolve, reject) => {
      // make a request to https://greenwichmeantime.com/timepiece/world-clock/
      fetch('https://greenwichmeantime.com/timepiece/world-clock/')
        .then(response => response.text()) // get the response as text
        .then(html => {
          // parse the HTML to extract the current time
          const parser = new DOMParser()
          const doc = parser.parseFromString(html, 'text/html')
          const timeElement = doc.querySelector('.current-time')
          if (timeElement) {
            // extract the time string from the element and return it
            const timeString = timeElement.textContent
            resolve(timeString)
          } else {
            // throw an error if the time element was not found
            reject(new Error('Time element not found'))
          }
        })
        .catch(error => {
          // reject the promise if there was an error with the request or parsing the HTML
          reject(error)
        })
    })
  }
}

Scratch.extensions.register(new ClockExtension())
