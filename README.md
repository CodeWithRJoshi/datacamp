# DataCamp

Directory per course with problems, instruction and solutions in markdown, dataset included, in a well-managed fashion.

## General Format

### Some Question Text
More question text

#### Instructions
- Do this
- DO That

<details>
<summary>Hints</summary>

- Here's how you do this
- Get it?
```
    Here's the code
```
</details>

<details>
<summary>Solution</summary>

```python
    print('Put solution here!')
```
</details>

### Markdown for the above format:

```markdown
### Some Question Text
More question text

#### Instructions
- Do this
- DO That

<details>
<summary>Hints</summary>

- Here's how you do this
- Get it?
    ```
        Here's the code
    ```
</details>

<details>
<summary>Solution</summary>

    ```python
        print('Put solution here!')
    ```
</details>


```
Mind the blank line after *\<summary\>* tag. 

Not all tools render html within the markddown. For this reason, question and the instruction shouldn't be in an accordion. Solution is an acceptable inconvenience when using such tools.
