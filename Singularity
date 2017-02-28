# Run MRIQC inside singularity image
BootStrap: docker
From: poldracklab/neuroimaging-core:base-0.0.2

%runscript
	mriqc "$@"

%post
# Download/install miniconda3
	curl -sSLO https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
        /bin/bash Miniconda3-latest-Linux-x86_64.sh -b -p /usr/local/miniconda && \
        rm Miniconda3-latest-Linux-x86_64.sh
# make some mount points
	mkdir /om
	mkdir /scratch
# create conda environment
	conda config --add channels conda-forge && \
	conda install -y numpy>=1.12.0 scipy matplotlib && \
	python -c "from matplotlib import font_manager"
# write out to global environment    
	echo "
	export PATH=/usr/local/miniconda/bin:$PATH
	export PYTHONPATH=/usr/local/miniconda/lib/python3.5/site-packages
	export PYTHONNOUSERSITE=1
	export LANG=C.UTF-8
	export LC_ALL=C.UTF-8    

	. /etc/fsl/fsl.sh
	. /etc/afni/afni.sh
	    
	" >> /environment
# install latest mriqc and requirements
	pip install https://github.com/poldracklab/mriqc/archive/master.zip
