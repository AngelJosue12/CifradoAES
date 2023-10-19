<template>

  <div>

    <h1>Cifrado AES</h1>

    <div>
      <label>Texto a cifrar:</label> 
      <input v-model="plaintext" />
    </div>

    <div>
      <label>Texto cifrado:</label>
      <input v-model="ciphertext" readonly />
    </div>

    <button @click="encryptText">Cifrar</button>

    <div>
      <label>Texto cifrado a descifrar:</label>
      <input v-model="ciphertextToDecrypt" /> 
    </div>

    <div>
      <label>Texto descifrado:</label>
      <input v-model="decryptedText" readonly />
    </div>

    <button @click="decryptText">Descifrar</button>

  </div>

</template>

<script>

import AES from 'crypto-js/aes';
import Utf8 from 'crypto-js/enc-utf8';
  
export default {

  data() {
    return {
      plaintext: '',
      ciphertext: '',
      ciphertextToDecrypt: '',
      decryptedText: ''  
    }
  },

  methods: {

    encryptText() {
  const passphrase = 'secret key 123';

  // Cifrar texto plano
  const ciphertext = AES.encrypt(this.plaintext, passphrase).toString();
  console.log('Ciphertext:', ciphertext);

  this.ciphertext = ciphertext;
},

decryptText() {
  const passphrase = 'secret key 123';

  // Descifrar texto cifrado
  const bytes = AES.decrypt(this.ciphertextToDecrypt, passphrase);
  console.log('Bytes:', bytes);

  // Decodificar bytes
  this.decryptedText = bytes.toString(Utf8);
}

  }

}

</script>