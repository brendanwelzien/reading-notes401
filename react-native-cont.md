# Creating a Responsive React Native Layout

```js
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default class App extends React.Component {
    render(){
        return(
            <View style={styles.container}>
                <Text> Hello world </Text>
            </View>
        );
    }
}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
    }
});
```
- change export for the component you want to add... such as header, boxes, footer, etc.
- react formatting is treated through flexbox styling like on the web
