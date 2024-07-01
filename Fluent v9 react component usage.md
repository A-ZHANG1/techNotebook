### Fluent v9 react component usage
#### Fluent UI repository folder structure
The Fluent UI repository on GitHub is organized into several key directories and packages, each serving distinct purposes. Here’s an overview of its structure:

1. apps: This directory contains non-published packages primarily used for internal purposes, such as testing and the website.
2. packages: This is the core of the repository where most of the published packages reside. These packages cover various aspects from styling, theming, utilities, to the main components of the Fluent UI React library. Notable subdirectories include:
    - @fluentui/react: Exports official components intended for long-term support. It often re-exports components from other packages to avoid circular dependencies.
    - @fluentui/react-northstar: Contains components mainly used by the Teams web application. It also includes utilities associated with these components.
    - @fluentui/react-component: These packages (like react-button, react-input, etc.) contain components that utilize the new composition and styling approaches of Fluent UI v9.
3. scripts: This directory contains scripts used for building and managing the monorepo. It supports the inner loop build system essential for development workflows.
4. specs: Contains technical specifications for various components. While not frequently updated, it provides foundational documentation for component development.
5. typings: Includes custom type definitions for global types and packages without official TypeScript declarations.

The repository also includes several utility packages that support component development:

- @fluentui/merge-styles: The existing styling solution used in many components.
- @fluentui/make-styles: Experimental styling solutions aimed at solving current issues with existing styles.
- @fluentui/style-utilities: Styling helpers required by most components.
- @fluentui/utilities: Basic utility functions used across components.
- @fluentui/theme: Building blocks for creating themes consumed by Fluent UI React components.
#### Customize fluent v9 TagPicker
The react-tag-picker folder in the Fluent UI repository primarily contains the components and logic for the Tag Picker control. This control is used for selecting tags from a predefined list, often with support for features like search, filtering, and custom rendering.

1. TagPicker Component:

Combines multiple sub-components to create the tag selection experience.
Handles displaying selected tags and providing a UI for searching and adding new tags.
2. TagPickerControl:

Manages the input field and the button to trigger the tag picker dropdown.
3. TagPickerList:

Displays the list of tag options that can be selected, filtered based on the search input.
4. TagPickerOption & TagPickerOptionGroup:

Represents individual selectable tag options and groups of options, respectively.
5. State Management:

Uses hooks to manage the selected tags, the search input value, and the open/close state of the dropdown.
6. Event Handling:

onOptionSelect: Handles the selection of a tag from the list.
Prevents event bubbling to avoid closing the dropdown when interacting with the search box.
##### Key Points:
Preventing Event Bubbling: This is necessary to ensure that clicking on the search box doesn’t trigger the dropdown to close. It allows for uninterrupted typing and filtering of tags.
Focus Handling: Keeping focus on the search box helps in maintaining user experience, allowing seamless tag search and selection without the dropdown closing unexpectedly.

##### Example:
Try from [stackblitz](https://stackblitz.com/edit/noa3xd-vdwvat?file=src%2Fexample.tsx)
```typescript

const fieldRef = React.useRef<HTMLDivElement>(null);
const handleClickOutside = (event: any) => {
    if (fieldRef.current && !fieldRef.current.contains(event.target)) {
        if (isPickerOpen) setIsPickerOpen(false);
    }
};
React.useEffect(() => {
    document.addEventListener('click', handleClickOutside);
    return () => {
        document.removeEventListener('click', handleClickOutside);
    };
}, [isPickerOpen]);

return (<Field
    ref={fieldRef}
    tabIndex={100}
    label={<Label weight='semibold' required={true}>''Example</Label>}
    onClick={() => {if (!isPickerOpen) setIsPickerOpen(true);}}
    >
            <TagPicker
                aria-labelledby={algTagPickerId}
                selectedOptions={tMLAlgs.concat(sparkAlgs)}
                onOptionSelect={onOptionSelect}
                open={isPickerOpen}
                inline={true}
                positioning='below'
            >
                <TagPickerControl className={styles.modelInput}>
                    <TagGroup
                        onDismiss={removeItem}
                        aria-label='Dismiss example'
                        className={styles.modelTagGroup}
                        role='listbox'
                    >
                        {tMLSelectedAlgs.concat(sparkSelectedAlgs).map((option) => (
                            <Tag
                                key={option}
                                value={option}
                                dismissible={true}
                                shape='rounded'
                                size='small'
                                dismissIcon={{ 'aria-label': 'remove' }}
                                role='option'
                            >
                                {option}
                            </Tag>
                        ))}
                    </TagGroup>
                    <TagPickerButton aria-label='Select Algorithms'/>
                </TagPickerControl>

                <TagPickerList className={styles.modelList}>
                    <SearchBox
                        className={styles.modelSearchBox}
                        ref={searchBoxRef}
                        placeholder={SR.SearchAvailableAlgs}
                        value={searchValue}
                        onChange={(ev: SearchBoxChangeEvent, data: InputOnChangeData) => {
                            if (data !== undefined) {
                                setSearchValue(data.value);
                            }
                        }}
                        onClick={(e) => {
                            searchBoxRef.current?.focus();
                            e.stopPropagation();
                        }}
                    />
                    <TagPickerOptionGroup label={SR.AutoMLAlgTraditional} className={styles.options}>
                        {validateSearch(AllChecked.allTML, searchValue, AllChecked.allTML) &&
                        <TagPickerOption value={AllChecked.allTML} key={AllChecked.allTML} className={styles.option} text=''>
                            <Checkbox
                                label={<Body1Strong>{SR.AutoMLAlgTraditionalAll}</Body1Strong>}
                                checked={areAllChecked(AllChecked.allTML)}
                            />
                        </TagPickerOption>}
                        {...tMLAlgs.map((option) =>
                            validateSearch(option, searchValue, AllChecked.allTML) && (
                                <TagPickerOption value={option} key={`tml-${option}`} className={styles.option} text=''>
                                    <Checkbox
                                        key={option}
                                        label={option}
                                        checked={tMLSelectedAlgs.includes(option)}
                                    />
                                </TagPickerOption>
                            )
                        )}
                    </TagPickerOptionGroup>
                    <TagPickerOptionGroup label={SR.AutoMLAlgSpark} className={styles.options}>
                        {validateSearch(AllChecked.allSpark, searchValue, AllChecked.allSpark) &&
                        <TagPickerOption value={AllChecked.allSpark} key={AllChecked.allSpark}
                            className={styles.option}
                            text=''
                        >
                            <Checkbox
                                label={<Body1Strong>{SR.AutoMLAlgSparkAll}</Body1Strong>}
                                checked={areAllChecked(AllChecked.allSpark)}
                            />
                        </TagPickerOption>}
                        {...sparkAlgs.map((option) =>
                            validateSearch(option, searchValue, AllChecked.allSpark) &&
                                <TagPickerOption value={option} key={`spark-${option}`} className={styles.option} text=''>
                                    <Checkbox
                                        key={option}
                                        label={option}
                                        checked={sparkSelectedAlgs.includes(option)}
                                    />
                                </TagPickerOption>
                        )}
                    </TagPickerOptionGroup>
                </TagPickerList>
            </TagPicker>
        </Field>
```
##### Reference
* Accessibility: https://tabster.io/docs/concept/
* doc: 
* code:
