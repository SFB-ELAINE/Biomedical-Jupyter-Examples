###############################################################################
# Biomedical-Jupyter-Examples is licensed under a
# Creative Commons Attribution 4.0 International License.
#
# You should have received a copy of the license along with this
# work. If not, see <http://creativecommons.org/licenses/by/4.0/>.
###############################################################################

FROM jupyter/minimal-notebook:45f07a14b422

LABEL maintainer="openscience.elaine@uni-rostock.de"

# Set user to Jupyter Notebook user
USER $NB_USER

# Change working directory to volume mount point
WORKDIR /home/$NB_USER/work

# Copy requirements file from host to temp directory
COPY requirements.txt /tmp/requirements.txt

# Install requirements
RUN python3 -m pip install -r /tmp/requirements.txt
