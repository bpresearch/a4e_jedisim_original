1. Introduction and implementation

Please refer to the documentations:
jedisim5/documentation/jedisim/jedisim.pdf
jedisim5/documentation/lensing/lensing.pdf


2. Configuration

Modify your settings in jedisim5/physics_settings/.

2.1 Lens parameter

Modify the lens parameter file "lens*.txt". 

Modify the file name of "lens*.txt" in "config" or "config_grid" correspondingly. 

Format of lens parameter file "lens*.txt": x y type p1 p2
    where x - x center of lens (in pixels)
        y - y center of lens (in pixels)
        type - type of mass profile
	    1. Singular isothermal sphere
	    2. Navarro-Frenk-White profile
	    3. NFW constant distortion profile for grid simulations
        p1 - first profile parameter
	    1. sigma_v [km/s]
	    2. M200 parameter [10^14 solar masses]
	    3. Distance to center in pixels. M200 fixed at 20 default, which can be modified in case 3
        p2 - second profile parameter
	    1. not applicable, can take any numerical
	    2. concentration parameter [dimentionless]
	    3. concentration parameter [dimentionless]

We recommend to use type=2 (NFW profile) for cluster simulations, and type=1 (SIS profile) for grid simulations. 

2.2 Configuration file

Modify the configuration file "config" for cluster simulation or "config_grid" for grid simulation.

Include the PSF file into the "physics_settings/" folder, and specify the PSF file name in the configuration file.

The simulation output is rescaled from HST pixel scale to the final pixel scale set in the configuration file. 

For grid simulations: 
Set the grid_radius (in pixels) and grid_angle (in radian) in the configuration file.
Set sigma_v (in km/s) in the lens parameter file. 
Make sure the grid_radius is smaller than half of the image size. 


3. Usage

In "jedisim5/" folder:

python jedimaster.py physics_settings/config


4. Output

Specify the directory of output images (eg. "trial_1/") in the output settings section of "config" file.

Specify the output prefix (eg. "trial1_") in the output settings section of "config" file.

There are corresponding simulation output in which the galaxies are 90 degree rotated in output directory (eg. "90_trial_1/").


5. Others

The original images and radius/redshift data are in "jedisim5/simdatabase/". 

The source codes are in "jedisim5/sources/".

Other parameters can be modified in "jedisim5/sources/jedidistort.c" (eg. OMEGA_M, G, H0). 

If any modifications are made in "jedisim5/source/" folder, delete the UNIX executable files in "jedisim5/" (jedicatalog, jediconvolve, jedidistort, jedigrid_a, jedigrid_b, jedinoise, jedipaste, jedirescale, jeditransform) and regenerate them. 