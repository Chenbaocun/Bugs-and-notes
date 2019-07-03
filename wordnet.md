# WordNet相关
1. path_similarity：寻找两个synset的最低公共上位词节点，计算common_hypernym到两个synset的路径之和，相似度=1/(path+1)。ps：当两个synset是同一个的时候，path为0，为保证分母不为0，在分母中加1。
2.
