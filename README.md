# react-native-signature-pad

[![npm version](https://badge.fury.io/js/react-native-signature-pad.svg)](//npmjs.com/package/react-native-signature-pad)
[![star this repo](http://githubbadges.com/star.svg?user=kevinstumpf&repo=react-native-signature-pad&style=flat)](https://github.com/kevinstumpf/react-native-signature-pad) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) [![All Contributors](https://img.shields.io/badge/all_contributors-12-orange.svg?style=flat-square)](#contributors) [![Known Vulnerabilities](https://snyk.io/test/github/kevinstumpf/react-native-signature-pad/badge.svg?style=flat-square)](https://snyk.io/test/github/kevinstumpf/react-native-signature-pad) 

React Native wrapper around @[szimek's](https://github.com/szimek) HTML5 Canvas based [Signature Pad](https://github.com/szimek/signature_pad)

- Supports Android and iOS
- Pure JavaScript implementation with no native dependencies
- Tested with RN 0.20
- Can easily be rotated using the "transform" style
- Generates a base64 encoded png image of the signature
- **Forked and fixed for ActivityIndicator from props**
- **Added Clean button**

## Demo

![SignaturePadDemo](https://cloud.githubusercontent.com/assets/7293984/13297035/303fefc6-dae5-11e5-99e8-edb8335633b5.gif) ![SignaturePadDemoAndroid](https://cloud.githubusercontent.com/assets/7293984/13299954/72bc3bf4-daf2-11e5-8606-388c05c26d6d.gif)

## Installation

```sh
$ yarn add wievtsal/react-native-signature-pad
```

## Example

```js
import React, {Component} from 'react';
import {View, ActivityIndicator, StyleSheet, TouchableOpacity, Text} from 'react-native';
import SignaturePad from 'react-native-signature-pad';

export default class Join extends Component {
  state = {
    signaturePadKey: 0
  };

  render = () => {
    return (
      <View style={styles.conteiner}>
        {this.createSignaturePad()}
        <TouchableOpacity onPress={this.cleanButtonAction} style={styles.btn}>
          <Text>Clean</Text>
        </TouchableOpacity>
      </View>
    );
  };

  _signaturePadError = error => {
    console.error(error);
  };

  _signaturePadChange = ({base64DataUrl}) => {
    console.log('Got new signature: ' + base64DataUrl);
  };

  createSignaturePad = () => {
    return (
      <View style={{height: 200}}>
        <SignaturePad
          key={this.state.signaturePadKey}
          onError={this._signaturePadError}
          onChange={this._signaturePadChange}
          onLoading={() => <ActivityIndicator style={styles.loadingIndicator} />}
          style={styles.signaturePad}
        />
      </View>
    );
  };

  cleanButtonAction = () => {
    this.setState({signaturePadKey: this.state.signaturePadKey + 1, signature: null});
  };
}

const styles = StyleSheet.create({
  conteiner: {
    flex: 1,
    padding: 15,
    marginTop: 45
  },
  loadingIndicator: {
    position: 'absolute',
    left: 0,
    right: 0,
    top: 0,
    bottom: 0,
    alignItems: 'center',
    justifyContent: 'center'
  },
  signaturePad: {
    flex: 1,
    backgroundColor: '#fff',
    borderWidth: 1,
    borderRadius: 6,
    borderColor: '#cecece'
  },
  btn: {
    padding: 10,
    backgroundColor: '#cecece',
    width: 200,
    borderRadius: 6,
    alignSelf: 'center',
    marginTop: 15,
    alignItems: 'center'
  }
});
```
