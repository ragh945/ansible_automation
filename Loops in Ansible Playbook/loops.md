# Ansible Loops Explained with Python Equivalents

This guide shows how **loops in Ansible** compare to **loops in
Python**, with simple examples.

------------------------------------------------------------------------

## 🔹 Example 1: Add several users (simple list)

**Ansible:**

``` yaml
- name: add several users in one go
  user:
    name: "{{ item }}"
    state: present
    groups: "games"
  loop:
    - testuser1
    - testuser2
    - testuser3
    - testuser4
    - testuser5
```

**Python equivalent:**

``` python
users = ["testuser1", "testuser2", "testuser3", "testuser4", "testuser5"]

for item in users:
    print(f"Creating user {item} in group games")
```

------------------------------------------------------------------------

## 🔹 Example 2: Add several users with groups (list of dictionaries)

**Ansible:**

``` yaml
- name: add several users with groups
  user:
    name: "{{ item.name }}"
    state: present
    groups: "{{ item.groups }}"
  loop:
    - { name: 'testuser6', groups: 'nobody' }
    - { name: 'testuser7', groups: 'nobody' }
    - { name: 'testuser8', groups: 'postfix' }
    - { name: 'testuser9', groups: 'postfix' }
```

**Python equivalent:**

``` python
users = [
    {"name": "testuser6", "groups": "nobody"},
    {"name": "testuser7", "groups": "nobody"},
    {"name": "testuser8", "groups": "postfix"},
    {"name": "testuser9", "groups": "postfix"},
]

for item in users:
    print(f"Creating user {item['name']} in group {item['groups']}")
```

------------------------------------------------------------------------

## 🔹 Example 3: Loop over two lists together

**Ansible:**

``` yaml
- name: Loop Over Two Lists Together
  debug:
    msg: "{{ item.0 }} and {{ item.1 }}"
  loop: "{{ alpha | zip(numbers) | list }}"
```

**Python equivalent:**

``` python
alpha = ["a", "b", "c", "d"]
numbers = [1, 2, 3, 4]

for a, n in zip(alpha, numbers):
    print(f"{a} and {n}")
```

------------------------------------------------------------------------

## ✅ Summary in Python terms

-   `loop:` in Ansible = `for item in list:` in Python.\
-   `item` in Ansible = loop variable in Python.\
-   `with_together` (old style) = `zip(list1, list2)` in Python.\
-   Dictionaries in loops work the same (`item['key']` in Python =
    `item.key` in Ansible).

------------------------------------------------------------------------

# **OUTPUTS**:
## 🔹 Example 1: Simple list of users
- Creating user testuser1 in group games
- Creating user testuser2 in group games
- Creating user testuser3 in group games
- Creating user testuser4 in group games
- Creating user testuser5 in group games

## 🔹 Example 2: Users with groups (dictionaries)
- Creating user testuser6 in group nobody
- Creating user testuser7 in group nobody
- Creating user testuser8 in group postfix
- Creating user testuser9 in group postfix

## 🔹 Example 3: Two lists zipped together
- a and 1
- b and 2
- c and 3
- d and 4
