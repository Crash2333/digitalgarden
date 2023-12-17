---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/Exception/ComposeException001/","tags":["JetpackCompose/Exception"],"noteIcon":""}
---

## TextField设置高度后，内容被挤压遮挡显示不完整
```kotlin
        TextField(
            value = username,
            singleLine = true,
            modifier = Modifier.fillMaxWidth().height(43.dp),
            colors = TextFieldDefaults.textFieldColors(
                unfocusedIndicatorColor = Color(0xffdddddd),
                backgroundColor = Color.White
            ),
            onValueChange = { username = it }
        )
```

当这个输入框的高度小于56dp时，就会出现文字显示不完整的问题。
## 原因分析
出现这个情况的原因是因为 TextField 中包含了一个 contentPadding，设置了内容离边界的距离。

## 解决方案
魔改TextField代码自定义EditText来控制内容边距。

```
@OptIn(ExperimentalMaterial3Api::class)  
@Composable  
fun EditText(  
    value: String,  
    onValueChange: (String) -> Unit,  
    modifier: Modifier = Modifier,  
    enabled: Boolean = true,  
    readOnly: Boolean = false,  
    textStyle: TextStyle = LocalTextStyle.current,  
    label: @Composable (() -> Unit)? = null,  
    placeholder: @Composable (() -> Unit)? = null,  
    leadingIcon: @Composable (() -> Unit)? = null,  
    trailingIcon: @Composable (() -> Unit)? = null,  
    supportingText: @Composable (() -> Unit)? = null,  
    isError: Boolean = false,  
    visualTransformation: VisualTransformation = VisualTransformation.None,  
    keyboardOptions: KeyboardOptions = KeyboardOptions.Default,  
    keyboardActions: KeyboardActions = KeyboardActions.Default,  
    singleLine: Boolean = false,  
    maxLines: Int = Int.MAX_VALUE,  
    interactionSource: MutableInteractionSource = remember { MutableInteractionSource() },  
    shape: Shape = TextFieldDefaults.filledShape,  
    colors: TextFieldColors = TextFieldDefaults.textFieldColors(),  
    paddingValues: PaddingValues = PaddingValues(0.dp)  
) {  
    // If color is not provided via the text style, use content color as a default  
    /* val textColor = textStyle.color.takeOrElse {         colors.textColor(enabled).value     }     val mergedTextStyle = textStyle.merge(TextStyle(color = textColor))*/  
    @OptIn(ExperimentalMaterial3Api::class)  
    BasicTextField(  
        value = value,  
        modifier = modifier  
            .defaultMinSize(  
                minWidth = TextFieldDefaults.MinWidth,  
                minHeight = TextFieldDefaults.MinHeight  
            ),  
        onValueChange = onValueChange,  
        enabled = enabled,  
        readOnly = readOnly,  
//            textStyle = mergedTextStyle,  
//            cursorBrush = SolidColor(colors.cursorColor(isError).value),  
        visualTransformation = visualTransformation,  
        keyboardOptions = keyboardOptions,  
        keyboardActions = keyboardActions,  
        interactionSource = interactionSource,  
        singleLine = singleLine,  
        maxLines = maxLines,  
        decorationBox = @Composable { innerTextField ->  
            // places leading icon, text field with label and placeholder, trailing icon  
            TextFieldDefaults.TextFieldDecorationBox(  
                value = value,  
                visualTransformation = visualTransformation,  
                innerTextField = innerTextField,  
                placeholder = placeholder,  
                label = label,  
                leadingIcon = leadingIcon,  
                trailingIcon = trailingIcon,  
                supportingText = supportingText,  
                shape = shape,  
                singleLine = singleLine,  
                enabled = enabled,  
                isError = isError,  
                interactionSource = interactionSource,  
                colors = colors,  
                contentPadding = paddingValues  
            )  
        }  
    )  
}
```




## 参考资料