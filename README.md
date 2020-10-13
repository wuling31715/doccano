# doccano

doccano is an open source text annotation tool for human. It provides annotation features for text classification, sequence labeling and sequence to sequence. So, you can create labeled data for sentiment analysis, named entity recognition, text summarization and so on. Just create project, upload data and start annotation. You can build dataset in hours.

## Demo

You can enjoy [annotation demo](http://doccano.herokuapp.com).

### [Named entity recognition](https://doccano.herokuapp.com/demo/named-entity-recognition/)

First demo is one of the sequence labeling tasks, named-entity recognition. You just select text spans and annotate it. Since doccano supports shortcut key, so you can quickly annotate text spans.

![Named Entity Recognition](./docs/named_entity_annotation.gif)

## Features

* Collaborative annotation
* Language independent
* (future) Auto labeling

## Requirements

* Python 3.6+
* Django 2.0.5+
* Node.js v14.13.0+
* npm 6.14.8+
* Vue.js
* Google Chrome(highly recommended)

## Deployment

First of all, you have to clone the repository:

```bash
git clone https://github.com/wuling31715/doccano.git
cd doccano
```

Next we need to install the dependencies. Run the following commands:

```bash
pip install -r requirements.txt
cd app
```

Next we need to compile the frontend. Run the following commands:

```bash
cd server
npm install
npm run build
cd ..
```

Next we need to make migration. Run the following command:

```bash
python manage.py migrate
```

Next we need to create a user who can login to the admin site. Run the following command:


```bash
python manage.py createsuperuser
```

Enter your desired username and press enter.

```bash
Username: admin
```

You will then be prompted for your desired email address:

```bash
Email address: admin@example.com
```

The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.

```bash
Password: **********
Password (again): *********
Superuser created successfully.
```

## Usage

### Start the development server

Let’s start the development server and explore it.

```bash
python manage.py runserver [port] // default = 8000
```

Now, open a Web browser and go to <http://127.0.0.1:8000/login/>. You should see the login screen:

<img src="./docs/login_form.png" alt="Login Form" width=400>

### 1. Create a project

Now, try logging in with the superuser account you created in the previous step. You should see the doccano project list page:

<img src="./docs/projects.png" alt="projects" width=600>

There is no project created yet. To create your project, make sure you’re in the project list page and select `Create Project` button. You should see the following screen:

<img src="./docs/create_project.png" alt="Project Creation" width=400>

In this step, you can select three project types: text classificatioin, sequence labeling and sequence to sequence. You should select a type with your purpose.

### 2. Define labels

Click `Labels` button in left bar to define your own labels. You should see the label editor page. In label editor page, you can create labels by specifying label text, shortcut key, background color and text color.

<img src="./docs/label_editor.png" alt="Edit label" width=600>

### 3. Import Data

After creating a project, you will see the "Import Data" page, or click `Import Data` button in the navigation bar. You should see the following screen:

<img src="./docs/upload.png" alt="Upload project" width=600>

You can upload two types of files:
- `CSV file`: file must contain a header with a `text` column or be one-column csv file.
- `JSON file`: each line contains a JSON object with a `text` key. JSON format supports line breaks rendering. (recommended)

> Notice: Doccano won't render line breaks in annotation page for sequence labeling task due to the indent problem, but the exported JSON file still contains line breaks.

`example.txt` (or `example.csv`)
```python
EU rejects German call to boycott British lamb.
President Obama is speaking at the White House.
He lives in Newark, Ohio.
...
```
`example.json`
```JSON
{"text": "EU rejects German call to boycott British lamb."}
{"text": "President Obama is speaking at the White House."}
{"text": "He lives in Newark, Ohio."}
...
```

Any other columns (for csv) or keys (for json) are preserved and will be exported in the `metadata` column or key as is.

Once you select a TXT/JSON file on your computer, click `Upload dataset` button. After uploading the dataset file, we will see the `Dataset` page (or click `Dataset` button list in the left bar). This page displays all the documents we uploaded in one project.

### 4. Annotation

Now, you are ready to annotate the texts. Just click the `Annotate Data` button in the navigation bar, you can start to annotate the documents you uploaded.

<img src="./docs/annotation.png" alt="Edit label" width=600>

### 5. Export Data

After the annotation step, you can download the annotated data. Click the `Edit data` button in navigation bar, and then click `Export Data`. You should see below screen:

<img src="./docs/export_data.png" alt="Edit label" width=600>

You can export data as CSV file or JSON file by clicking the button. As for the export file format, you can check it here: [Export File Formats](https://github.com/chakki-works/doccano/wiki/Export-File-Formats). 

Each exported document will have metadata column or key, which will contain
additional columns or keys from the imported document. The primary use-case for metadata is to allow you to match exported data with other system
by adding `external_id` to the imported file. For example:

Input file may look like this:
`import.json`
```JSON
{"text": "EU rejects German call to boycott British lamb.", "external_id": 1}
```
and the exported file will look like this:
`output.json`
```JSON
{"doc_id": 2023, "text": "EU rejects German call to boycott British lamb.", "labels": ["news"], "username": "root", "metadata": {"external_id": 1}}
```
### 6. Manage Data

If you want to manage data. Click the `Admin` button in navigation bar. You should see below screen:

<img src="./docs/delete_data.png" alt="Delete Data">

### Tutorial

We prepared a NER annotation tutorial, which can help you have a better understanding of doccano. Please first read the README page, and then take the tutorial. [A Tutorial For Sequence Labeling Project](https://github.com/chakki-works/doccano/wiki/A-Tutorial-For-Sequence-Labeling-Project).

I hope you are having a great day!

## Contribution

As with any software, doccano is under continuous development. If you have requests for features, please file an issue describing your request. Also, if you want to see work towards a specific feature, feel free to contribute by working towards it. The standard procedure is to fork the repository, add a feature, fix a bug, then file a pull request that your changes are to be merged into the main repository and included in the next release.

Here are some tips might be helpful. [How to Contribute to Doccano Project](https://github.com/chakki-works/doccano/wiki/How-to-Contribute-to-Doccano-Project)


## Contact

For help and feedback, please feel free to contact [the author](https://github.com/Hironsan).

**If you are favorite to doccano, please follow my [GitHub](https://github.com/Hironsan) and [Twitter](https://twitter.com/Hironsan13) account.**
