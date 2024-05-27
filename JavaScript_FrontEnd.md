#### JS中难以理解的概念
1. closure 闭包和链式作用域
2. this的指向对象和需要var that = this的情况
3. 变量提升
4. JS异步与callBack回调函数
5. event loop和事件委托
6. 函数即对象。高阶函数：返回函数的函数
7. 原型，原型链，原型继承
8. 严格模式 strict mode
```
会把一个component渲染两次
React官方：Now that this reducer function is pure, calling it an extra time doesn’t make a difference in behavior. This is why React calling it twice helps you find mistakes.
要求多次的call pure function结果相同
```
10. 对象


# 维护一个可变长的`<TextArea>`组成的table(`<DataGrid>` of [FluentV9](https://github.com/microsoft/fluentui))

## Overview

This document provides a detailed explanation of the usage of the `Textarea` component within the `EditTagPanelBody` component. The key focus is on the integration with `ref` and `DataGrid` components to handle dynamic content updates and maintain consistent user experience.

## Key Logic

### Ref Management

#### Purpose

The `ref` is used to manage the `Textarea` instances efficiently, allowing direct manipulation of DOM elements for updating their styles dynamically.

#### Implementation

Each `Textarea` component is assigned a `ref` that is stored in the component's state. This allows the application to dynamically adjust the height of each `Textarea` based on its content.

##### Example:

```typescript
interface IRowProps {
    key: string;
    value: string;
    idx: string;
    keyErrorMessage?: string;
    valueErrorMessage?: string;
    // 正在变更item时不允许同时新增再次调用setItem
    loading?: boolean;
    // 更改key的时候用来删除旧的Key
    oldKey?: string;
    // 维护table中单元格的高度
    buttonWrapperRef: React.RefObject<HTMLDivElement>;
    keyTextareaRef: React.RefObject<HTMLTextAreaElement>;
    valueTextareaRef: React.RefObject<HTMLTextAreaElement>;
}
```

```typescript
const updateHeight = (ta: React.RefObject<HTMLTextAreaElement>) => {
    ta.current!.style.height = 'auto';
    ta.current!.style.height = `${ta.current!.scrollHeight}px`;
};
```

This function is used to adjust the height of the `Textarea` elements dynamically whenever the content changes.

### DataGrid Integration

#### Purpose

`DataGrid` is used to display a list of tags that can be edited by the user. The `Textarea` components are embedded within `DataGrid` cells to facilitate inline editing.

#### Implementation

The `DataGrid` component is configured with columns that render `Textarea` components for the tag `key` and `value` fields.

##### Example:

```typescript
const tableColumns: TableColumnDefinition<IRowProps>[] = React.useMemo(() => [
    createTableColumn<IRowProps>({
        columnId: 'name',
        renderHeaderCell: () => {
            return 'Name';
        },
        renderCell: (item) => {
            return (
                <TableCellLayout>
                    <Field
                        validationMessage={item.keyErrorMessage ?  item.keyErrorMessage : item.loading ? 'Loading' : undefined}
                        validationState={item.keyErrorMessage ? 'error' : 'none'}
                        validationMessageIcon={item.keyErrorMessage ? <ErrorCircle12Filled /> :
                            item.loading ? <Spinner size='extra-tiny'/> : null}
                    >
                        <Textarea
                            textarea={{
                                className: styles.textArea,
                                ref: item.keyTextareaRef,
                            }}
                            defaultValue={item.key}
                            onChange={( e: React.ChangeEvent, data: TextareaOnChangeData ) => {
                                item.key = data.value.trim();
                                onUpdateRow(item);
                            }}
                            onBlur={() => {onBlurRow(item);}}
                            rows={1}
                        />
                    </Field>
                </TableCellLayout>
            );
        },
    }),
    createTableColumn<IRowProps>({
        columnId: 'value',
        renderHeaderCell: () => {
            return 'Value';
        },
        renderCell: (item) => {
            return <TableCellLayout>
                <Field
                    validationMessage={item.valueErrorMessage}
                >
                    <Textarea
                        textarea={{
                            className: styles.textArea,
                            ref: item.valueTextareaRef,
                        }}
                        defaultValue={item.value}
                        onChange={( e: React.ChangeEvent, data: TextareaOnChangeData ) => {
                            item.value = data.value.trim();
                            onUpdateRow(item);
                        }}
                        onBlur={() => {onBlurRow(item);}}
                        rows={1}
                    />
                </Field>
            </TableCellLayout>;
        },
    }),
], [items]);
```

### Key Functionalities

#### Dynamic Height Adjustment

To ensure the `Textarea` components grow with the content, the `updateHeight` function is invoked on component mount and whenever the content changes. This is handled within a `useEffect` hook to manage updates efficiently.

#### Validation and Error Handling

Each `Textarea` is wrapped in a `Field` component that displays validation messages. The validation logic checks for empty fields and whitespace issues, updating the component state to reflect errors.

##### Example:

```typescript
const onBlurRow = async(item: IRowProps) => {
    const currentTag = items[findIndexByIdx(items, item.idx)];

    // Empty key is not allowed
    if (item.key === '') {
        currentTag.keyErrorMessage = SR.TagKeyValidationMessage2;
    } else if (currentTag.keyErrorMessage !== SR.TagKeyValidationMessage1) {
        currentTag.keyErrorMessage = '';
    }
    // Empty value is forbidden by the backend
    if (item.value === '') {
        currentTag.valueErrorMessage = SR.TagKeyValidationMessage2;
    } else {
        currentTag.valueErrorMessage = '';
    }

    // Update data
    if (!item.keyErrorMessage && !item.valueErrorMessage) {
        // Update run tag
        currentTag.key = item.key;
        currentTag.value = item.value;
        currentTag.loading = true;
        setItems([...items]);
        try {
            if (item.oldKey && item.oldKey !== item.key) await onDeleteTag(item.oldKey);
            await onSetTag({ key: item.key, value: item.value }).then(() => {
                currentTag.loading = false;
            });
        } catch (error: unknown) {
            currentTag.keyErrorMessage = (error as Error).message;
        }
        setItems([...items]);
    }

    setItems([...items]);
};
```

### Conclusion

The integration of `Textarea` components within the `EditTagPanelBody` leverages `ref` and `DataGrid` to provide a dynamic and user-friendly interface for editing tags. The `ref` management ensures the `Textarea` components adapt to content changes, while `DataGrid` facilitates efficient rendering and interaction. Validation and error handling mechanisms further enhance the robustness of the component.
