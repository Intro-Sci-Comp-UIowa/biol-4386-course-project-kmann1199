# Setup

```
%pylab inline
from spring_helper import *
from doublet_detector import *
from collections import defaultdict
Populating the interactive namespace from numpy and matplotlib
plt.rcParams['font.family'] = 'sans-serif'
plt.rcParams['font.sans-serif'] = 'Arial'
plt.rc('font', size=14)
plt.rcParams['pdf.fonttype'] = 42
Download data
```
 #Download raw data by navigating to the following URL in your web browser:
 #http://cf.10xgenomics.com/samples/cell-exp/2.1.0/pbmc8k/pbmc8k_filtered_gene_bc_matrices.tar.gz

 #Or use wget
 #!wget http://cf.10xgenomics.com/samples/cell-exp/2.1.0/pbmc4k/pbmc4k_filtered_gene_bc_matrices.tar.gz
 #Uncompress 
 #!tar xfz pbmc4k_filtered_gene_bc_matrices.tar.gz
```
%cd data_prep/
/home/houston_common/Software/SPRING_dev-master/data_prep
!ls
```
doublet_detector.py
doublet_detector.pyc
filtered_gene_bc_matrices
helper_functions.py
pbmc4k_filtered_gene_bc_matrices.tar.gz
raw_counts
spring_example_HPCs.ipynb
spring_example_pbmc4k.ipynb
spring_example_tropWT_heads-Copy1.ipynb
spring_example_tropWT_heads.ipynb
spring_helper.py
spring_helper.pyc
spring_notebook_10X_CITEseq.ipynb
spring_notebook_10X.ipynb
# Load data
```
input_path = 'filtered_gene_bc_matrices/Xtro9_1'
if os.path.isfile(input_path + '/matrix.npz'):
    E = scipy.sparse.load_npz(input_path + '/matrix.npz')
else:
    E = scipy.io.mmread(input_path + '/matrix.mtx').T.tocsc()
    scipy.sparse.save_npz(input_path + '/matrix.npz', E, compressed=True)

print E.shape
```
(6914, 19983)
```
gene_list = np.array(load_genes(input_path + '/features.tsv', delimiter='\t', column=1))
gene_list
```
 array(['ebi3', 'pacrgl', 'atoh8', ..., 'ENSXETG00000040209',
       'ENSXETG00000038429', 'ENSXETG00000041280'], dtype='|S37')
```
total_counts = E.sum(1).A.squeeze()  #gene counts per cell
E = tot_counts_norm(E)[0]
```
#Save base directory files
 #Set path for saving data -- you'll have to change this for your own setup.
 #This path should be a subdirectory of your local copy of SPRING,
 #specifically, {path_to_SPRING}/datasets/{main_dataset_name}. 
 #See example below, where springViewer_1_6_dev.html is located in ../
```
main_spring_dir = '../datasets/trop/'

if not os.path.exists(main_spring_dir):
    os.makedirs(main_spring_dir)
```
```
np.savetxt(main_spring_dir + 'genes.txt', gene_list, fmt='%s')
np.savetxt(main_spring_dir + 'total_counts.txt', total_counts)
```
 # save master expression matrices
```
print 'Saving hdf5 file for fast gene loading...'
save_hdf5_genes(E, gene_list, main_spring_dir + 'counts_norm_sparse_genes.hdf5')
```
```
print 'Saving hdf5 file for fast cell loading...'
save_hdf5_cells(E, main_spring_dir + 'counts_norm_sparse_cells.hdf5')
```
```
save_sparse_npz(E, main_spring_dir + 'counts_norm.npz', compressed = False)
scipy.io.mmwrite(main_spring_dir + 'matrix.mtx', E)
```
Saving hdf5 file for fast gene loading...
Saving hdf5 file for fast cell loading...
#Save SPRING files
```
t0 = time.time()

save_path = main_spring_dir + 'full'

out = make_spring_subplot(E, gene_list, save_path, 
                    normalize = False, tot_counts_final = total_counts,
                    min_counts = 3, min_cells = 3, min_vscore_pctl = 85,show_vscore_plot = True, 
                    num_pc = 30, 
                    k_neigh = 4, 
                    num_force_iter = 500)

np.save(save_path + '/cell_filter.npy', np.arange(E.shape[0]))
np.savetxt(save_path + '/cell_filter.txt',  np.arange(E.shape[0]), fmt='%i')

print 'Finished in %i seconds' %(time.time() - t0)
```
/home/houston_common/miniconda/envs/spring/lib/python2.7/site-packages/matplotlib/font_manager.py:1331: UserWarning: findfont: Font family [u'sans-serif'] not found. Falling back to DejaVu Sans
  (prop.get_family(), self.defaultFamily[fontext]))

<img width="443" alt="MeanVariancePlot" src="https://user-images.githubusercontent.com/124283697/235753678-37236979-f2c1-4aa0-8c01-c32de5239dd9.png">

Finished in 48 seconds
 
