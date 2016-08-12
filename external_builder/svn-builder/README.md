# openshift-svn-builder
OpenShift 3 Docker Builder which fetches sources from Subversion

The included template `svn-builder.json` helps to create applications based on this builder.

## Template Parameters
The included template `svn-builder.json` supports the following parameters:

  * APPLICATION_NAME: Name of the created application
  * SOURCE_REPOSITORY: URL of SVN repository. The builder expects to find `Dockerfile` and Docker context in the root directory of the working copy.
  
## Usage

Register the template on OpenShift:

    oc create -n openshift -f https://raw.githubusercontent.com/gabrielscheffer/osev3-examples/master/external_builder/svn-builder/svn-builder.json

Create build based on template:

    oc process -n openshift svn-builder -v 'TEMPLATE_ARGUMENTS' | \
        oc create -f -

e.g.:

    oc process -n openshift svn-builder -f svn-builder -v 'APPLICATION_NAME=myapp,SOURCE_REPOSITORY=https://svn.yourcompany.com/gabrielscheffer/product/trunk' | \
        oc create -f -
