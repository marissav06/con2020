# Con2020 - Current Sheet Model Code

This repository contains IDL and MATLAB code for the Connerney et al. (2020) Jupiter current sheet model. This is part of a community code project: [Magnetospheres of the Outer Planets Group Community Code](https://lasp.colorado.edu/mop/missions/juno/community-code). For Python versions, please see the [stand alone code](https://github.com/gabbyprovan/con2020/), or the [JupiterMag](https://github.com/mattkjames7/JupiterMag) package. 

**Citation DOI**: <a href="https://doi.org/10.5281/zenodo.6981615">10.5281/zenodo.6981615</a> (for all releases)
Each version release also has its own DOI, click the link above to get to the DOI of specific versions.

**Journal Paper DOI**: <a href="https://doi.org/10.1007/s11214-023-00961-3">https://doi.org/10.1007/s11214-023-00961-3</a> (PDF via DOI, or <a href="https://rdcu.be/c5I71">https://rdcu.be/c5I71</a>)

This code provides <b>only the magnetic field due to the current sheet</b>. For the full magnetospheric field one should include a model for Jupiter's internal magnetic field, such as VIP4 or JRM09. You can find IDL code for the JRM09 internal field model here: https://github.com/marissav06/jovian_jrm09_internal

These codes were developed by Marty Brennan, Stan Cowley, Matt James, Aneesah Kamran, Gabby Provan, Marissa Vogt, and Rob Wilson, with thanks to Fran Bagenal, Jack Connerney, and Masafumi Imai. The codes are intended for use by the Juno science team and other members of the planetary magnetospheres community. Questions, corrections, or other comments can be shared with the authors by emailing mvogt@bu.edu.

These codes uses a right-handed System III (1965) (SYSIII) co-ordinate system (Cartesian or Spherical), and assumes that 1 jovian radius (R<sub>J</sub>) = 71,492 km.


<h3><b>Running the code</b><ul></h3>
  <li><b>con2020_model_rtp</b> calls <b>con2020_model_xyz</b>, so download both files locally.
  <li>With default current sheet model parameter structure:  <b>B = con2020_model_rtp(eq_type, r_rj, colat_rads, elong_rads)</b></li>
  <li>With user-specified current sheet parameters:
    <ul>
      <li>Obtain the default model parameters: <b>params = con2020_model_rtp('default_values')</b></li>
      <li>Edit the structure to adjust the model parameters as you wish, e.g. <b>params.r1__outer_rj = 50.0</b><br>(sets outer edge to 50 R<sub>J</sub>; default is 51.4 R<sub>J</sub>)</li>
      <li>Call the function with the adjusted parameter structure: <b>B = con2020_model_rtp(eq_type, r_rj, colat_rads, elong_rads, params)</b></li>
    </ul></li>
  <li>For cartesian input/output, use <b>B = con2020_model_xyz(eq_type, x_rj, y_rj, z_rj)</b></li>
  </ul>
  
<h3><b>Required Inputs</b></h3>
  <ul>
  <li>eq_type - Whether to use the integral or analytic versions of the model equations. Options are 'integral', 'analytic' or 'hybrid', or set to 'default_values' to return a structure of all default values.</li>
  <li>Position - format depends on whether user is running <b>con2020_model_rtp</b> or <b>con2020_model_xyz</b>
    <ul><li>For spherical input:<ul>
      <li>r_rj - radial distance, in R<sub>J</sub>. Value(s) must be 0 < r_rj < 200.</li>
      <li>colat_rads - colatitude, in radians. Value(s) must be 0 <= colat_rads <= pi.</li>
      <li>elong_rads - East longitude, right handed, in radians. Value(s) must be 0 <= elong_rads <= 2pi.</li></ul>
    <li>For cartesian input:<ul>
      <li>x_rj - SYSIII x position, in R<sub>J</sub>, Values must be -200 < x_rj < 200.</li>
      <li>y_rj - SYSIII y position, in R<sub>J</sub>, Values must be -200 < x_rj < 200.</li>
      <li>z_rj - SYSIII z position, in R<sub>J</sub>, Values must be -200 < x_rj < 200.</li></ul>
    <li>Note: for spherical input, r_rj, colat_rads and elong_rads can be scalars or 1D arrays, but only one eq_type. For cartesian input, x_rj, y_rj and z_rj can be scalars or 1D arrays, but only one eq_type. For MATLAB, the 1D arrays must be size (n x 1), not (1 x n).</li>  
    </ul>
    </ul>
   

      

<h3><b>Optional inputs (e.g. in structure con2020_model_rtp('default_values'))</b></h3>
<table>
  <tr><b>
    <th>Variable name</th>
    <th>Description</th>
    <th>Default value</th></b>
  </tr>
  <tr>
    <td>mu_i_div2__current_parameter_nT</td>
    <td>mu0i0/2 term (current sheet field parameter)</td>
    <td>139.6 nT</td>
  </tr>
  <tr>
    <td>i_rho__radial_current_MA</td>
    <td>radial current term from Connerney et al., 2020 (set this to zero to turn radial currents off as in Connerney et al. 1981)</td>
    <td>16.7 MA</td>
  </tr>
  <tr>
    <td>r0__inner_rj</td>
    <td>inner edge of current disk in R<sub>J</sub></td>
    <td>7.8 R<sub>J</sub></td>
  </tr>
  <tr>
    <td>r1__outer_rj</td>
    <td>outer edge of current disk in R<sub>J</sub></td>
    <td>51.4 R<sub>J</sub></td>
  </tr>
  <tr>
    <td>d__cs_half_thickness_rj</td>
    <td>D, current sheet half thickness</td>
    <td>3.6 R<sub>J</sub></td>
  </tr>
  <tr>
    <td>xt__cs_tilt_degs</td>
    <td>current sheet tilt angle</td>
    <td>9.3 degrees</td>
  </tr>
  <tr>
    <td>xp__cs_rhs_azimuthal_angle_of_tilt_degs</td>
    <td>azimuthal angle of the current sheet tilt (right handed)</td>
    <td>155.8 degrees right handed (corresponds to 204.2 degrees left handed longitude)</td>
  </tr>
  <tr>
    <td>error_check</td>
    <td>1 to check that inputs are valid (Default), or set to 0 to skip input checks (faster)</td>
    <td>1</td>
  </tr>
</table>
  
<h3><b>Outputs</b></h3>
<ul>
  <li>The code outputs a vector that contains the 3 components of the magnetic field produced by the current sheet, in SIII right-handed.</li>
  <li>For con2020_model_rtp (spherical input/output) the vector is [Br, Btheta, Bphi] in nT.</li>
  <li>For con2020_model_xyz (cartesian input/output) the vector is [Bx, By, Bz] in nT.</li>
  </ul>   

<h3>History</h3>
This repository was made by merging a previous <a href="https://github.com/marissav06/con2020_idl">IDL specific</a> and a <a href="https://github.com/marissav06/con2020_matlab">Matlab specific</a> repository.

<h4>References:</h4>
<ul>
<li>Connerney, J. E. P., Acuña, M. H., & Ness, N. F. (1981). Modeling the Jovian current sheet and inner magnetosphere. Journal of Geophysical Research, 86, 8370-8384. https://doi.org/10.1029/JA086iA10p08370</li>
<li>Connerney, J. E. P., Timmins, S., Herceg, M., & Joergensen, J. L. (2020). A Jovian magnetodisc model for the Juno era. Journal of Geophysical Research: Space Physics, 125, e2020JA028138. https://doi.org/10.1029/2020JA028138</li>
<li>Edwards, T. M., Bunce, E. J., & Cowley, S. W. H. (2001). A note on the vector potential of Connerney et al.'s model of the equatorial current sheet in Jupiter's magnetosphere. Planetary and Space Science, 49, 1115– 1123. https://doi.org/10.1016/S0032-0633(00)00164-1</li>
  <li>Wilson, R.J., Vogt, M.F., Provan, G. et al. Internal and External Jovian Magnetic Fields: Community Code to Serve the Magnetospheres of the Outer Planets Community. Space Sci Rev 219, 15 (2023). https://doi.org/10.1007/s11214-023-00961-3</li>
</ul>
