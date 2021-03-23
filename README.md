# PDF signer Brazil

A JavaScript PDF signer with certificate CPF and CNPJ A1 ICP-Brasil for NodeJS. 

This package is fork of [vizicsaba89/pdf-signer](https://github.com/vizicsaba89/pdf-signer).

## PDF versions
Pdf-signer cant handle pdf stream in the moment. It only can works with pdf which built on XREF tables. 


## Installation

Installation uses the npm package manager. Just type the following command after installing npm.

```bash
npm install pdf-signer-brazil
```

## Usage

single signing example:
```javascript
import { sign } from 'pdf-signer-brazil'
const fs = require('fs')
const dateFormat = require("dateformat")

const p12Buffer = fs.readFileSync(`./assets/pdf-signer.p12`) // CPF/CNPJ A1 ICP-Brasil: Use original .pfx file 
const pdfBuffer = fs.readFileSync(`./assets/example.pdf`)

const signature = 'Your Name'
const password = 'pdfsigner'
const signedPdf = sign.sign(pdfBuffer, p12Buffer, password, {
  reason: 'Test',
  email: 'mail@mail.com',
  location: 'City, BR',
  signerName: signature,
  annotationAppearanceOptions: {
    signatureCoordinates: { left: 20, bottom: 120, right: 190, top: 20 },
    signatureDetails: [
      {
        value: signature,
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 32 },
      },
      {
        value: 'Este arquivo foi assinado digitalmente',
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 25.4 },
      },
      {
        value: 'Assinado em ' + dateFormat(new Date(), 'd/mm/yyyy HH:mm:ss'),
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 18 },
      },
      {
        value: 'Verifique o arquivo em verificador.iti.gov.br',
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 11 },
      },
    ]
  },
})
signedPdf.then(content => fs.writeFileSync('./assets/results/signed.pdf', content))
```
More examples can be found in spec file [spec](https://github.com/willmdrs/pdf-signer-brazil/blob/master/src/sign.spec.ts).

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
