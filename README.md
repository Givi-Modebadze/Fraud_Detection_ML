IEEE-CIS Fraud Detection
	* კონკურსის მიზანია მანქანური სწავლების სხვადასხვა მეთოდის გამოყენება სავარაუდო Fraud- ის შესახებ პროგნოზის გასაკეთებლად.
	
	* პრობლემის გადასაწყვეტად გამოვიყენე Cleaning, Feature Engineering და Feature Selection - ის სხვადასხვა მიდგომა და შემდეგი მოდელები: Logistic Regression, Random Forest, Decision Trees და XGBoost.

რეპოზიტორიის სტრუქტურა:
	* model_experiment_Logistic_Regression: 
		ხდება მონაცემების Cleaning, Feature Engineering და Feature Selection.
		გასუფთავებისთვის უბრალოდ ისეთ სვეტებს რომლებსაც NAN მნიშვნელობების რაოდენობა 90% ზე მეტი აქვთ ვყრი და დარჩენილ NAN მნიშვნელობებს მოდით ვანაცვლებ.
		Feature Engineering-თვის ვიყენებ LabelEncoder-ს და StandardScaler-ს.
		Feature Selection-თვის ვიყენებ SelectKBest-ს რათა ნაკლებად მნიშვნელოვანი მონაცემები გადავყარო.
		
	* model_experiment_Random_Forest:
		Cleaning იგივე რაც Logistic_Regression-ში
		Feature Engineering სკალირებას არ საჭიროებს ამიტომ მხოლოდ LabelEncoder
		Feature Selection საჭირო არ არის რადგან  მოდელი თავად არჩევს საუკეთესო პარამეტრებს.
		
	* model_experiment_Decision_Tree:
		Cleaning: იგივე რაც Logistic_Regression-ში 90%-ის ნაცვლად 80% ვცადე.
		Feature Engineering: OrdinalEncoder
		Feature Selection: არა
	
	* model_experiment_xgboost: 
		Cleaning: 90%
		Feature Engineering: OrdinalEncoder
		Feature Selection: არა
		
		
	* model_inference: ტესტ სეტზე პროგნოზი ხდება საუკეთესო მოდელის გამოყენებით
	
	* submission
	
	* README 
	
Feature Engineering
	* სვეტები რომელთაც ზედმეტად ბევრი NAN მნიშვნელობა ჰქონდა გადავყარე (80%, 90%)
	
	* NAN მნიშვნელობები ჩავანაცვლე მოდით, შეიძლებოდა საშუალოს ან მედიანის გამოყენება, თუმცა ჩემი აზრით, მოდა ყველაზე ლოგიკურია.
	
	* კატეგორიული ცვლადების რიცხვითში გადასაყვანად გამოვიყენე (LabelEncoder, OrdinalEncoder) 
	
	* ასევე StandardScaler მონაცემების დასასკალირებლად.
	

Feature Selection
	* გამოვიყენე SelectKBest სხვადასხვა პარამეტრებით, უნდა აღინიშნოს, Random_Forest, Decision_Tree და xgboost კარგ შედეგს დებს Feature Selection-ის გარეშეც.
	
Training
	* Logistic Regression, Random Forest, Decision Trees და XGBoost
	
	* Hyperparameter-ების შესარჩევად აქაც და სხვა მოდელების შემთხვევაშიც რამდენიმე სხვადასხვა მოდელი გავტესტე. იმის მიხედვით overfitting ან underfitting ხდებოდა თუ არა შევეცადე ოპტიმალური პარამეტრების შერჩევას.
	
	* საუკეთესო შედეგი ჰქონდა XGBoost-ს. ეს მოდელი ყველაზე უკეთ მოერგო მოცემულ მონაცემებს. 
	
MLflow Tracking
	* ექსპერიმენტების ბმული: https://dagshub.com/Givi-Modebadze/Fraud_Detection_ML.mlflow/#/experiments/0?searchFilter=&orderByKey=attributes.start_time&orderByAsc=false&startTime=ALL&lifecycleFilter=Active&modelVersionFilter=All+Runs&datasetsFilter=W10%3D
	
	* თითოეული მოდელისთვის შენახული მაქვს მხოლოდ roc_auc_train და roc_auc_test.
	
	* საბოლოო მოდელის ლინკი: https://dagshub.com/Givi-Modebadze/Fraud_Detection_ML.mlflow/#/experiments/3/runs/51704e8765134ee5bfc3a533bfda57ca/artifacts
	
	* საბოლოოდ შეირჩა XGBoost შემდეგი პარამეტრებით: 
		reg_alpha: 0.1
		max_depth: 5
		n_jobs: -1
		colsample_bytree: 0.7
		reg_lambda: 1.0
		subsample: 0.8
		tree_method: hist
		n_estimators: 500
		learning_rate: 0.1
		random_state: 42
	* შედეგი: 
		roc_auc_test: 0.8908687871894844
		roc_auc_train: 0.9633058123162956
	* submission score:
		Public Score: 0.921531
