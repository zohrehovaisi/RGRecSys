# RGRecSys
RGRecSys is developed using [RecBole library](https://github.com/RUCAIBox/RecBole) built-in models and covers several models from general and context-aware recommender systems. It has a robustness evaluation module that allows users to easily and uniformly evaluate recommender system robustness. 
## Requirements
As RGRecSys is built using the RecBole library, it has the same requirements as RecBole:

- python >= 3.7 
- torch >= 1.7.0
- numpy >= 1.17.2
- scipy == 1.6.0
- hyperopt >= 0.2.4
- pandas >= 1.0.5
- tqdm >= 4.48.2
- scikit_learn >= 0.23.2
- pyyaml >= 5.1.0
- colorlog == 4.7.2
- colorama == 0.4.4
- tensorboard >= 2.5.0

## Usage

1. If you want to use datasets other than ml-100k, you need to use recbole library to get the atomic files. Otherwise, you can skip this step. The atomic files provides a data representation for different recommendation algorithms including .INTER, .USER, and .ITEM. See [this](https://dl.acm.org/doi/abs/10.1145/3459637.3482016) for more information.
2. Download the recbole folder from v0.2.1 of RecBole library from [here](https://github.com/RUCAIBox/RecBole/archive/refs/tags/v0.2.1.zip) and locate it in the main folder you downloaded from our github (RGRecSys-master).
3. Create a folder names as "saved" in RGRecSys-master folder.
4. Specify the model, dataset, and desired robustness test in the main function of RobustnessGymRecSys.py follwing the example below:

if __name__ == '__main__':
all_results = {}
for model in [“BPR”]:  #Specify model here
dataset = "ml-100k"    #Specify dataset here
base_config_dict =     #Specify selectively loading data here. Keys are the suffix of loaded atomic files, values are the list of field names to be loaded
{
'load_col': {'inter': ['user_id', 'item_id',
'rating', 'timestamp'],
'user': ['user_id', 'age', 'gender',
'occupation'],
'item': ['item_id', 'release_year', 'class']}
}
robustness_dict =      #Specify the robustnes test here. This example shows slicing based on user feature
{
"slice": {
"by_feature": {
"occupation": {"equal": "student"}
}
}
}
results = train_and_test(model=model, dataset=dataset,
robustness_tests=robustness_dict,
base_config_dict=base_config_dict, save_model=False)

## Cite

If you aim to use RGRecSys for your research or development, please cite the following paper:


Zohreh Ovaisi, Shelby Heinecke, Jia Li, Yongfeng Zhang, Elena Zheleva, and Caiming Xiong. "RGRecSys: A Toolkit for Robustness Evaluation of Recommender Systems". In Proceedings of the Fifteenth ACM International Conference on Web Search and Data Mining (WSDM '22)
