# ebrahimtawfeeq.github.io
Supervised learning algorithm using decision tree diagram
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Import tools"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Get the data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>sepal_length</th>\n",
       "      <th>sepal_width</th>\n",
       "      <th>petal_length</th>\n",
       "      <th>petal_width</th>\n",
       "      <th>type</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>5.1</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>4.9</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>4.7</td>\n",
       "      <td>3.2</td>\n",
       "      <td>1.3</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4.6</td>\n",
       "      <td>3.1</td>\n",
       "      <td>1.5</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5.0</td>\n",
       "      <td>3.6</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>5.4</td>\n",
       "      <td>3.9</td>\n",
       "      <td>1.7</td>\n",
       "      <td>0.4</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>4.6</td>\n",
       "      <td>3.4</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.3</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>5.0</td>\n",
       "      <td>3.4</td>\n",
       "      <td>1.5</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>4.4</td>\n",
       "      <td>2.9</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>4.9</td>\n",
       "      <td>3.1</td>\n",
       "      <td>1.5</td>\n",
       "      <td>0.1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   sepal_length  sepal_width  petal_length  petal_width  type\n",
       "0           5.1          3.5           1.4          0.2     0\n",
       "1           4.9          3.0           1.4          0.2     0\n",
       "2           4.7          3.2           1.3          0.2     0\n",
       "3           4.6          3.1           1.5          0.2     0\n",
       "4           5.0          3.6           1.4          0.2     0\n",
       "5           5.4          3.9           1.7          0.4     0\n",
       "6           4.6          3.4           1.4          0.3     0\n",
       "7           5.0          3.4           1.5          0.2     0\n",
       "8           4.4          2.9           1.4          0.2     0\n",
       "9           4.9          3.1           1.5          0.1     0"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "col_names = ['sepal_length', 'sepal_width', 'petal_length', 'petal_width', 'type']\n",
    "data = pd.read_csv(\"iris.csv\", skiprows=1, header=None, names=col_names)\n",
    "data.head(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Node class"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "class Node():\n",
    "    def __init__(self, feature_index=None, threshold=None, left=None, right=None, info_gain=None, value=None):\n",
    "        ''' constructor ''' \n",
    "        \n",
    "        # for decision node\n",
    "        self.feature_index = feature_index\n",
    "        self.threshold = threshold\n",
    "        self.left = left\n",
    "        self.right = right\n",
    "        self.info_gain = info_gain\n",
    "        \n",
    "        # for leaf node\n",
    "        self.value = value"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Tree class"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "class DecisionTreeClassifier():\n",
    "    def __init__(self, min_samples_split=2, max_depth=2):\n",
    "        ''' constructor '''\n",
    "        \n",
    "        # initialize the root of the tree \n",
    "        self.root = None\n",
    "        \n",
    "        # stopping conditions\n",
    "        self.min_samples_split = min_samples_split\n",
    "        self.max_depth = max_depth\n",
    "        \n",
    "    def build_tree(self, dataset, curr_depth=0):\n",
    "        ''' recursive function to build the tree ''' \n",
    "        \n",
    "        X, Y = dataset[:,:-1], dataset[:,-1]\n",
    "        num_samples, num_features = np.shape(X)\n",
    "        \n",
    "        # split until stopping conditions are met\n",
    "        if num_samples>=self.min_samples_split and curr_depth<=self.max_depth:\n",
    "            # find the best split\n",
    "            best_split = self.get_best_split(dataset, num_samples, num_features)\n",
    "            # check if information gain is positive\n",
    "            if best_split[\"info_gain\"]>0:\n",
    "                # recur left\n",
    "                left_subtree = self.build_tree(best_split[\"dataset_left\"], curr_depth+1)\n",
    "                # recur right\n",
    "                right_subtree = self.build_tree(best_split[\"dataset_right\"], curr_depth+1)\n",
    "                # return decision node\n",
    "                return Node(best_split[\"feature_index\"], best_split[\"threshold\"], \n",
    "                            left_subtree, right_subtree, best_split[\"info_gain\"])\n",
    "        \n",
    "        # compute leaf node\n",
    "        leaf_value = self.calculate_leaf_value(Y)\n",
    "        # return leaf node\n",
    "        return Node(value=leaf_value)\n",
    "    \n",
    "    def get_best_split(self, dataset, num_samples, num_features):\n",
    "        ''' function to find the best split '''\n",
    "        \n",
    "        # dictionary to store the best split\n",
    "        best_split = {}\n",
    "        max_info_gain = -float(\"inf\")\n",
    "        \n",
    "        # loop over all the features\n",
    "        for feature_index in range(num_features):\n",
    "            feature_values = dataset[:, feature_index]\n",
    "            possible_thresholds = np.unique(feature_values)\n",
    "            # loop over all the feature values present in the data\n",
    "            for threshold in possible_thresholds:\n",
    "                # get current split\n",
    "                dataset_left, dataset_right = self.split(dataset, feature_index, threshold)\n",
    "                # check if childs are not null\n",
    "                if len(dataset_left)>0 and len(dataset_right)>0:\n",
    "                    y, left_y, right_y = dataset[:, -1], dataset_left[:, -1], dataset_right[:, -1]\n",
    "                    # compute information gain\n",
    "                    curr_info_gain = self.information_gain(y, left_y, right_y, \"gini\")\n",
    "                    # update the best split if needed\n",
    "                    if curr_info_gain>max_info_gain:\n",
    "                        best_split[\"feature_index\"] = feature_index\n",
    "                        best_split[\"threshold\"] = threshold\n",
    "                        best_split[\"dataset_left\"] = dataset_left\n",
    "                        best_split[\"dataset_right\"] = dataset_right\n",
    "                        best_split[\"info_gain\"] = curr_info_gain\n",
    "                        max_info_gain = curr_info_gain\n",
    "                        \n",
    "        # return best split\n",
    "        return best_split\n",
    "    \n",
    "    def split(self, dataset, feature_index, threshold):\n",
    "        ''' function to split the data '''\n",
    "        \n",
    "        dataset_left = np.array([row for row in dataset if row[feature_index]<=threshold])\n",
    "        dataset_right = np.array([row for row in dataset if row[feature_index]>threshold])\n",
    "        return dataset_left, dataset_right\n",
    "    \n",
    "    def information_gain(self, parent, l_child, r_child, mode=\"entropy\"):\n",
    "        ''' function to compute information gain '''\n",
    "        \n",
    "        weight_l = len(l_child) / len(parent)\n",
    "        weight_r = len(r_child) / len(parent)\n",
    "        if mode==\"gini\":\n",
    "            gain = self.gini_index(parent) - (weight_l*self.gini_index(l_child) + weight_r*self.gini_index(r_child))\n",
    "        else:\n",
    "            gain = self.entropy(parent) - (weight_l*self.entropy(l_child) + weight_r*self.entropy(r_child))\n",
    "        return gain\n",
    "    \n",
    "    def entropy(self, y):\n",
    "        ''' function to compute entropy '''\n",
    "        \n",
    "        class_labels = np.unique(y)\n",
    "        entropy = 0\n",
    "        for cls in class_labels:\n",
    "            p_cls = len(y[y == cls]) / len(y)\n",
    "            entropy += -p_cls * np.log2(p_cls)\n",
    "        return entropy\n",
    "    \n",
    "    def gini_index(self, y):\n",
    "        ''' function to compute gini index '''\n",
    "        \n",
    "        class_labels = np.unique(y)\n",
    "        gini = 0\n",
    "        for cls in class_labels:\n",
    "            p_cls = len(y[y == cls]) / len(y)\n",
    "            gini += p_cls**2\n",
    "        return 1 - gini\n",
    "        \n",
    "    def calculate_leaf_value(self, Y):\n",
    "        ''' function to compute leaf node '''\n",
    "        \n",
    "        Y = list(Y)\n",
    "        return max(Y, key=Y.count)\n",
    "    \n",
    "    def print_tree(self, tree=None, indent=\" \"):\n",
    "        ''' function to print the tree '''\n",
    "        \n",
    "        if not tree:\n",
    "            tree = self.root\n",
    "\n",
    "        if tree.value is not None:\n",
    "            print(tree.value)\n",
    "\n",
    "        else:\n",
    "            print(\"X_\"+str(tree.feature_index), \"<=\", tree.threshold, \"?\", tree.info_gain)\n",
    "            print(\"%sleft:\" % (indent), end=\"\")\n",
    "            self.print_tree(tree.left, indent + indent)\n",
    "            print(\"%sright:\" % (indent), end=\"\")\n",
    "            self.print_tree(tree.right, indent + indent)\n",
    "    \n",
    "    def fit(self, X, Y):\n",
    "        ''' function to train the tree '''\n",
    "        \n",
    "        dataset = np.concatenate((X, Y), axis=1)\n",
    "        self.root = self.build_tree(dataset)\n",
    "    \n",
    "    def predict(self, X):\n",
    "        ''' function to predict new dataset '''\n",
    "        \n",
    "        preditions = [self.make_prediction(x, self.root) for x in X]\n",
    "        return preditions\n",
    "    \n",
    "    def make_prediction(self, x, tree):\n",
    "        ''' function to predict a single data point '''\n",
    "        \n",
    "        if tree.value!=None: return tree.value\n",
    "        feature_val = x[tree.feature_index]\n",
    "        if feature_val<=tree.threshold:\n",
    "            return self.make_prediction(x, tree.left)\n",
    "        else:\n",
    "            return self.make_prediction(x, tree.right)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Train-Test split"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [],
   "source": [
    "X = data.iloc[:, :-1].values\n",
    "Y = data.iloc[:, -1].values.reshape(-1,1)\n",
    "from sklearn.model_selection import train_test_split\n",
    "X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=.2, random_state=41)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Fit the model"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "X_2 <= 1.9 ? 0.33741385372714494\n",
      " left:0.0\n",
      " right:X_3 <= 1.5 ? 0.427106638180289\n",
      "  left:X_2 <= 4.9 ? 0.05124653739612173\n",
      "    left:1.0\n",
      "    right:2.0\n",
      "  right:X_2 <= 5.0 ? 0.019631171921475288\n",
      "    left:X_1 <= 2.8 ? 0.20833333333333334\n",
      "        left:2.0\n",
      "        right:1.0\n",
      "    right:2.0\n"
     ]
    }
   ],
   "source": [
    "classifier = DecisionTreeClassifier(min_samples_split=3, max_depth=3)\n",
    "classifier.fit(X_train,Y_train)\n",
    "classifier.print_tree()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Test the model"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9333333333333333"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred = classifier.predict(X_test) \n",
    "from sklearn.metrics import accuracy_score\n",
    "accuracy_score(Y_test, Y_pred)"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
