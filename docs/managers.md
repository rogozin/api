# ���������

* [���������� ����� � ���� ���������](#dict)
* [���������� ���������](#add)
* [�������������� ���������](#edit)
* [�������� ���������](#delete)

��� ��������� ���������� ���������� �������������� ��� �������������. 
��� ����������� ��� � ������������ ������������ ������ `403 Forbidden`.

<a name="dict"></a>
## ���������� ����� � ���� ���������

### ������
`GET /employers/{employer_id}/manager_types`, ��� employer_id - ������������� ���������
 
### �����

������ ������:
```json
{
    "managers": [
        {
            'id': 'manager',
            'name': '��������',
            'allowed_permissions:': [
                {
                    'id': 1,
                    'name': 'can_create_vacancy'
                },
                {
                    'id': 2,
                    'name': 'can_view_resume_contacts'
                }
            ]
        }
    ]
}
```json

 ��� | ��� | ��������
 --- | --- | ---
 id | ������ | ������������� ���� ���������
 name | ������ | �������� ���� ���������
 allowed_permissions | ������ | ������ ��������� ����
 
� �������� allowed_permissions ���������� ������ ��������� ����:

 ��� | ��� | ��������
 --- | --- | ---
 id | ������ | ������������� �����
 name | ������ | �������� �����
 
### ������
* `404 Not found` - ������������ �� ������ ��� � ������������ ��� ����

<a name="add"></a>
## ���������� ���������

### ������
`POST /employers/{employer_id}/managers`, ��� employer_id - ������������� ���������

�� ���� �������� json. ������:

```json
{
    'last_name': '',
    'first_name': '',
    'middle_name': '',
    'manager_type': '',
}
```json

### �����

### ������

<a name="edit"></a>
## �������������� ���������

### ������

### �����

### ������

<a name="delete"></a>
## �������� ���������

### ������

### �����

### ������