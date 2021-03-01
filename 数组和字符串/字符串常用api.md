### 字符串常用api

int isalnum(int c); 判断字符c是否为数字或字母。是则返回非0，不是则返回0。

int tolower(int c); 将大写字符转化为小写字符。如果无法进行这样的转换，则不进行转换

int stoi(string s); 将字符串转为数字。如果字符串无法转为数字，则报错

string to_string(int val); 将数字转为字符串

string::iterator erase(string::iterator it);  为string移除迭代器指向的那个字符，返回下一个字符。注意，移除字符后，该迭代器就会失效。因此 常常写作it=str.erase(it)； 详见https://cloud.tencent.com/developer/article/1036816

