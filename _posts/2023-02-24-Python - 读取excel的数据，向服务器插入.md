

# Python - 读取excel的数据，向服务器插入

```python
import json

import xlrd
import requests


def read_excel():
    workbook = xlrd.open_workbook(r"D:\Downloads\用户数据模板.xlsx")
    print(f"包含的表单数量{workbook.nsheets}")
    print(f"表单的名称为{workbook.sheet_names()}")
    # 表单索引从0开始，获取第一个表单对象
    ds = workbook.sheet_by_index(0)
    print(workbook.sheets())
    print(ds.name)
    print(f"行数：{ds.nrows}")
    print(f"列数：{ds.ncols}")
    row: int = 1
    first_row = ds.row_values(rowx=0, start_colx=0, end_colx=None)
    print(f"表头:{first_row}")
    name_index = first_row.index("姓名")
    phone_index = first_row.index("手机")
    print(f"姓名的下标： {name_index}")
    print(f"手机号的下标： {phone_index}")
    while row < ds.nrows:
        row_value = ds.row_values(rowx=row, start_colx=0, end_colx=None)
        # print(row_value)
        name = row_value[name_index]
        phone = int(row_value[phone_index])
        print(f"姓名：{name},手机号: {phone}")
        add_user(name, phone)
        row += 1

    # while row < ds.nrows:
    #     print(ds.row_values(rowx=row, start_colx=0, end_colx=None))
    #     row += 1

    # print(ds.col_values(colx=0, start_rowx=1, end_rowx=None))


# 添加用户
def add_user(name: str, phone: str):
    url = '接口地址'
    headers = {
        'Content-Type': 'application/json',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) '
                      'Chrome/94.0.4606.61 Safari/537.36 ',
        'authorization': 'Basic c2FiZXI6c2FiZXJfc2VjcmV0',
        'blade-auth': 'XXXX '
    }

    body = {"account": f"{name}", "tenantName": "", "realName": f"{name}", "roleName": "", "deptName": "",
            "userTypeName": "", "userType": 1, "tenantId": "000000", "password": "123456", "password2": "123456",
            "name": f"{name}", "phone": f"{phone}", "email": "", "sex": "", "birthday": "", "statusName": "",
            "code": "", "roleId": "1535148319667490817", "deptId": "1531184201791483905",
            "postId": "1123598817738675208"}
    response = requests.post(url, data=json.dumps(body), headers=headers).json()
    print(response)
    return response


if __name__ == '__main__':
    read_excel()

```

