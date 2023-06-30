# <font color="IndianRed"> TITO (Classical Chinese Office Title Translation)</font>
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1UoG3QebyBlK6diiYckiQv-5dRB9dA4iv?usp=sharing/)

Our model <font color="cornflowerblue">TITO (Classical Chinese Office Title Translation) </font> is a Sequence to Sequence Classical Chinese language model that is intended to  <font color="IndianRed">translate a Classical Chinese office title into English</font>. This model is first inherited from the MarianMTModel, and finetuned using a 6,208 high-quality translation pairs collected CBDB group (China Biographical Database). 

### <font color="IndianRed"> How to use </font>

Here is how to use this model to get the features of a given text in PyTorch:

<font color="cornflowerblue"> 1. Import model and packages </font>
```python
from transformers import MarianMTModel, MarianTokenizer

device = torch.device('cuda')
model_name = 'cbdb/ClassicalChineseOfficeTitleTranslation'
tokenizer = MarianTokenizer.from_pretrained(model_name)
model = MarianMTModel.from_pretrained(model_name).to(device)
```

<font color="cornflowerblue"> 2. Load Data </font>
```python
# Load your data here
tobe_translated = ['講筵官','判司簿尉','散騎常侍','殿中省尚輦奉御']
```

<font color="cornflowerblue"> 3. Make a prediction </font>
```python
inputs = tokenizer(tobe_translated, return_tensors="pt", padding=True).to(device)
translated = model.generate(**inputs, max_length=128)
tran = [tokenizer.decode(t, skip_special_tokens=True) for t in translated]
for c, t in zip(tobe_translated, tran):
    print(f'{c}: {t}')
```
講筵官: Lecturer<br>
判司簿尉: Supervisor of the Commandant of Records<br>
散騎常侍: Policy Advisor<br>
殿中省尚輦奉御: Chief Steward of the Palace Administration<br>

### <font color="IndianRed">Authors </font>
Queenie Luo (queenieluo[at]g.harvard.edu)
<br>
Hongsu Wang
<br>
Peter Bol
<br>
CBDB Group

### <font color="IndianRed">License </font>
Copyright (c) 2023 CBDB

Except where otherwise noted, content on this repository is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0).
To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/ or
send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.
