FROM mcr.microsoft.com/devcontainers/go:1.20-bullseye
# FROM mcr.microsoft.com/devcontainers/go:0-${templateOption:imageVariant}


# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    ksh \
    neofetch 

# [Optional] Uncomment the next lines to use go get to install anything else you need
# USER vscode
# RUN go get -x <your-dependency-or-tool>
# USER root

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

# Add microsoft repo 
# https://learn.microsoft.com/en-us/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-ver16&tabs=debian18-install%2Calpine17-install%2Cdebian8-install%2Credhat7-13-install%2Crhel7-offline#18
RUN curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update

# # Install Microsoft odbc utilities for Busche-sql which requires the older driver.
RUN DEBIAN_FRONTEND=noninteractive ACCEPT_EULA=Y apt-get install -y msodbcsql17
RUN DEBIAN_FRONTEND=noninteractive ACCEPT_EULA=Y apt-get install -y mssql-tools
RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# # Install Microsoft odbc utilities for Azure SQL which requires the older driver.
RUN DEBIAN_FRONTEND=noninteractive ACCEPT_EULA=Y apt-get install -y msodbcsql18
RUN DEBIAN_FRONTEND=noninteractive ACCEPT_EULA=Y apt-get install -y mssql-tools18
RUN echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y unixodbc-dev

# Install Plex ODBC driver
# WORKDIR /install/odbc
# COPY ./install/odbc/PROGRESS_DATADIRECT_OPENACCESS_OAODBC_8.1.0.HOTFIX_LINUX_64.tar .
# RUN tar -xf PROGRESS_DATADIRECT_OPENACCESS_OAODBC_8.1.0.HOTFIX_LINUX_64.tar
# COPY ./install/odbc/PlexDriverInstall.py ./
# RUN python PlexDriverInstall.py 
# COPY ./install/odbc/odbc.ini /etc/
# COPY ./install/odbc/odbc64.ini /usr/oaodbc81/
# ENV LD_LIBRARY_PATH="/usr/oaodbc81/lib64"
# ENV OASDK_ODBC_HOME="/usr/oaodbc81/lib64"
# ENV ODBCINI="/usr/oaodbc81/odbc64.ini"
