Core Competencies in Computational Data Science
===============================================

This document guides the development of our *ScienceCore* curriculum. We should plan on introducing each of these Computational Data Science Core Competencies (CC) at least once in the curriculum; ideally, they will be reinforced multiple times. The Learning Outcomes are written as an evaluation of a learner’s future performance; i.e., the past or present-perfect tense is used to describe what a learner is or will be doing in the future to implement these best practices (e.g., “uses version control;” “creates backups”).

This is intended to be a guide for instructors and curriculum developers; to aid in thinking about what skills should be taught as part of a computer-based science course. This is not a guide for learners, though we welcome input and contributions from anyone.


CC1 - Project and Data Management
---------------------------------

### Learning Outcomes

- 1.1: Raw data are unmodified and kept separate from any processed derivatives or analysis results.
- 1.2: A project’s files are organized hierarchically and semantically. Raw data, processed data, code, and outputs are stored in separate folders.
- 1.3: Uses meaningful but brief filenames and folder names. Uses one of the following strategies: Timestamps, Process hierarchy, or Filename metadata.
- 1.4: Knows how to navigate a file system using both a graphical user interface (GUI) and a command-line interface (CLI).
- 1.5: Records relationships between code, results, and metadata, preferably by a filename convention.
- 1.6: Chooses appropriate, non-proprietary data file formats based on the size of data, its complexity, and who will access it.
- 1.7: Creates regular, automated back-ups of all code, documentation, and any derived results that can’t be easily re-created. Does not back-up raw data unless it can’t be reproduced.
- 1.8: Use lossless file compression for storage, when appropriate, and especially for transfer.
- 1.9: Creates appropriate metadata for all datasets, recording the creation date, primary data sources, fill values or valid ranges, units, …
- 1.10: Uses a package manager to install and manage software dependencies.


### CC1.1 - Keeping Raw Data Separate

“Results should be reproduced from the earliest digital data in the experiment, whether that is raw data coming from instruments or observations, or data as accessed from a secondary source. It defeats the purpose to supply a ‘cleaned’ version of the data if it is impossible to access the methodology of the cleaning, for example. The goal is that all data manipulations be made transparent, beginning with the initial version of the data with which the researcher started working” (Stodden & Miguez 2014). Presumably, the raw data are publicly available and can be downloaded from a user-friendly website. If not, you should supply the raw data in addition to your code and any important analysis results when publishing or sharing your work. Raw data should never be changed! Unit conversions, corrections, interpolation, aggregation, and other changes should all be performed as part of a reproducible computational workflow and the “cleaned” data should be stored separately.


### CC1.2 - Organizing Files and Folders

“Files can be organized in folders according to types of: data–databases, text, images, models, sound; research activities–interviews, surveys, focus groups; or material–data, documentation, publications” (Ven den Eynden et al. 2011).


### CC1.3 - Meaningful Filenames

“Good file names can provide useful cues to the content and status of a file, can uniquely identify a file and can help in classifying files” (Ven den Eynden et al. 2011). We recommend one of the following strategies:

- **Timestamps:** A timestamp in a filename is guaranteed to be unique and will give you some indication of when the file was first created, even if it is accidentally modified (i.e., if the “Last modified date” is changed). Of course, a conflict between the filename’s timestamp and “Last modified date” could potentially be confusing. If a timestamp is used for an analysis result, like a TIFF image of an important plot, the same timestamp could be used to identify the Python script that created that plot. We recommend using timestamps of the format `YYYYMMDD` (four-digit year, two-digit month, two-digit day), as timestamps in this format, when placed at the beginning of a filename, will also cause the files to be placed in chronological order. Example: `20230530_plot_air_temperature_by_station.py`
- **Process hierarchy:** Because a computational workflow is a series of steps, files or folders in your project directory could be labeled and ordered by task. For example, folder names like `01_process_raw_sensor_data` or filenames like `02_plot_diagnostics.py` clearly signal to you and others both the purpose of the folder/ file and its order in a workflow. This is a particularly good pattern to use when publishing a set of scripts used in generating results for a peer-reviewed paper. It will be much easier for reviewers or other researchers to reproduce your analysis steps in the right order.
- **Filename metadata:** As suggested by Van den Eynden et al. (2011), “file names can contain project acronyms, researchers’ initials, file type information, a version number, file status information and date.” Use any or all of these as needed. File type information should probably be limited to the file extension (e.g., `.csv`, `.tiff`, `.py`) and your project should only use a given file type for one thing, if possible.

In addition, use the following best practices when creating files:

- Avoid using spaces or dots in filenames, except for the dot that separates the file extension from the name of the file. Spaces in filenames create difficulties at the command line.
- Choose a systematic filename convention that uniquely identifies each file (Van den Eynden et al, 2011). Timestamps are one example, but for groups of files you may come up with your own system. For example, data files generated by different weather stations in different years should all be named something like `StationName_YYYY_raw.csv` where `StationName` is the (unique) name of the station and `YYYY` is the year.


### CC1.4 - Navigating a File System


### CC1.5 - Relating Code, Outputs, and Metadata

It’s important to know what code generated a given result. When assessing a scientific claim, we usually want to know its provenance, i.e., how that scientific result was generated: by what process, using what data, and under what conditions. This is a narrative about how you achieved your results, and “the most fundamental strategy for enabling others to reproduce a computational analysis is to provide a detailed, written description of the process” (Piccolo & Frampton 2016). While there are sophisticated tools available to enable tracking of provenance, there are simple practices you can adopt to track your scientific workflows (Stodden & Miguez 2014).

If you’re looking at a plot you generated weeks ago and notice something you want to change, it’s much easier to do so if you can identify the code file that generated the plot. Matching timestamps (SK1.3) or other filename conventions can help you keep track of what file generated what result. Alternatively, if your project is organized by discrete tasks (e.g., `01_process_raw_sensor_data`), then you may have sub-folders for code and (a small number of) outputs, so that it’s obvious the outputs were generated by the code. A research log (e.g., as a Word document) can also help you keep track of important analysis results as long as you also consistently record how they were generated. This can be as simple, e.g., as recording the file path of the Python script that produced a certain result or allowed you to make a certain claim (Sandve et al. 2013).

“Narrative descriptions should indicate the operating system(s), software dependencies, and analytical software that were used, and how to obtain them. In addition, narratives should indicate the exact software versions used, the order in which they were executed, and all non-default parameters that were specified” (Piccolo & Frampton 2016). Note that these details can be conveyed simply by packaging your analysis as research software to be installed. This may not require more than a series of Python scripts, external or automatically generated documentation (e.g., from docstrings), and a well-established, one-step procedure for installing dependencies (e.g., using a setup.py file).

Davison (2012) provides a comprehensive list of the details needed to establish scientific provenance: the processing unit (architecture, word size, byte order); the operating system and version; for compiled code, the compilation procedure including compiler options, compilation order, all shared libraries and methods of linking them; for interpreted code, all dependencies; any virtual machine details, if relevant; the source and identity of any (raw) input datasets; and, finally, the output data, for evaluation and comparison to any reproduced results.


### CC1.6 - Appropriate Data File Formats

“For many projects, a small number of data tables will be generated that can be effectively managed with commercial or open source spreadsheet programs like Excel and OpenOffice Calc. Larger data volumes and usage constraints may require the use of relational database management systems” (Michener et al. 2015). But in addition to file size, you need to consider complexity and the needs of other users. Spreadsheets are relatively easy to use but are not appropriate for very complex datasets.

Plain-text comma-separated value (CSV) files, with self-descriptive column names, should generally be used instead of spreadsheets (Michener 2015), as text formatting and the row-column layout in spreadsheets can be meaningful in ways that are hard to communicate and harder for computers to understand. CSV column names should be self-descriptive, for example, by containing the units of measurement (e.g., `air_temp_celsius`). Consider your data users, as well. Multiple CSV files may seem unwieldy but are much easier to use than a database or a hierarchical data file (e.g., HDF5, netCDF4). When sharing data that were previously stored in a relational database, each table should be stored as a separate file (Costello & Wieczorek 2014).

Delimited text files like comma-separated value (CSV) files are both machine-readable and human-readable (they can be opened in a spreadsheet program), which means that data do not need to be duplicated or reformatted for different purposes. If contextual information needs to be provided (e.g., a detailed description of the column names, units, etc.), it should be provided either: 1) As plain text above the column header, with each line preceded by a comment character, likely the hash symbol (#); or, preferably 2) As a separate file in the same directory. Column names in your delimited text file should not contain spaces or special characters.


### CC1.7 - Regular Backups

If something terrible happens to your computer or a networked file system, or files are accidentally deleted, you could lose months of work! Make sure to backup any files you can’t afford to lose, preferably using a cloud-based solution. Services like Dropbox, Box, Microsoft OneDrive, and Google Drive can be used to automatically backup important files. Because derived results should be easy to generate again if you have the same code and (raw) data (see CC5.2), it’s not strictly necessary to backup results.

Choose a backup format that is easy to use and widely adopted. Platform-specific binary files (e.g., R’s `*.rda` format or Python’s `pickle` format) should be avoided for long-term backups because they may be difficult to open on a different computer, if the computer on which they created is unavailable or broken.


### CC1.8 - File Compression

File compression can be used to reduce file sizes and should be used whenever data will be transferred or downloaded. Some types of compression can permanently change data values. If compression is used, lossless compression should always be chosen, as it will preserve original data values. For example, a TIFF (`.tif`, `.tiff`) with LZW compression is a lossless alternative to JPEG (`.jpg`, `.jpeg`) files, as the latter will distort data values. If compressing a file archive that other people may use, use ZIP instead of less-compatible formats like 7zip, bzip, or xz.


### CC1.9 - Metadata


### CC1.10 - Software Package Management


---

CC2 - Scientific Programming
----------------------------

- 2.1: Understands how machines represent numbers.
- 2.2: Understands multidimensional arrays and their use for representing datasets structured by space, time, and multiple variables.
- 2.3: Writes vectorized code when working with arrays.
- 2.4: Understands when and how to generate random numbers and specifies the random seed when reporting results.
- 2.5: Profiles the resource use of a computational workflow.
- 2.6: Understands different types of concurrency and how to scale up a computational workflow that is limited by throughput or memory.
- 2.7: Can debug a computational workflow, either by deduction, print statements, breakpoints, or an interactive debugger.
- 2.8: Understands the difference in how computers read text files versus binary files and is familiar with reading both file types.
- 2.9: Familiar with the different types of structured datasets used in scientific applications, including spatial datasets (raster and vector) and  hierarchical datasets (e.g., HDF5, netCDF4); how to read them; and how to create self-documenting data files.


### CC2.1 - Machine Representation of Numbers

### CC3.2 - Multidimensional Arrays

### CC3.3 - Vectorized Code

### CC3.4 - Random Numbers and Seeds

### CC3.5 - Resource Profiling

### CC3.6 - Concurrency for Scale

As transistor manufacturing approaches physical limits for the size and heat dissipation of the most fundamental computational unit, increases in computational power are more dependent on multi-threaded and multi-process computing, rather than clock speeds (Rüde et al. 2018).


### CC3.7 - Debugging

### CC3.8 - Character Encoding and Reading Files

Some data files can be too large to fit into your computer’s memory. Even if they do fit in memory, it might be extremely difficult or slow to work with them using graphical applications like a spreadsheet program, as these programs typically read the entire file into memory when they are opened. Instead, programming languages offer the ability to read in one part of the file at a time.

- Binary files are typically read-in one byte (8 bits) at a time, though you can specify a multiple of bytes to be read if it represents a certain kind of number (e.g., a 32-bit integer).
- Text files are typically read-in one line at a time. Your programming environment will automatically convert bytes to text characters based on the file’s character encoding, but it may have to guess the encoding and it may be wrong.

Whether reading a binary file or a text file, in most languages, once you open a file for reading, you can only read each part of the file exactly once. The file reading operation only moves forward, so every byte or every line you read cannot be read again until you close and re-open the file. This leads to a potentially confusing situation for new programmers: You’ve opened the file and read it once but when you try to read it again, you get zero lines or zero bytes back. This is because the file reader has a pointer indicating which part you’re reading at any time, and that pointer only moves forward unless you deliberately indicate that it should go backward. This requires “seeking” a certain byte, e.g., the first byte in the file, which sets the pointer back at the beginning.


### CC3.9 - Spatial and Hierarchical Datasets


---

CC3 - Collaborative Computational Science
-----------------------------------------

- 3.1: Uses source control management (SCM) or version control to track changes to research software or scripts.
- 3.2: Make a project’s scripts or other computer artifacts publicly available in a way that enables other scientists to identify licensing, track different versions, make contributions, and re-use computational workflows.
- 3.3: One or more example workflows are provided for any reusable code.
- 3.4: Creates and documents how to install research software and the details of the software environment used, either by using virtual environments, build tools, or containers.
- 3.5: Any published data and code are assigned versions and given unique digital identifiers, preferably digital object identifiers (DOIs).
- 3.6: Knows how to read API documentation and where to go for help. Creates minimal working examples when sharing code that needs to be debugged or improved.
- 3.7: Uses consistent and legible coding style, probably informed by a language-specific standard or linting program.
- 3.8: Chooses variable names that are clear and informative.


### CC3.1 - Source Control Management

“Although scripts and code may be included alongside a manuscript as supplementary material, a better alternative is to store them in a public repository with a permanent URL” (Piccolo & Frampton 2016).


### CC3.2 - Publishing Code

Public software repositories include [SourceForge](http://sourceforge.net/), [Savannah](http://savannah.gnu.org/), [Bitbucket](https://bitbucket.org/), and [GitHub](https://github.com/). Increasingly, sharing code (and data) is becoming the standard by peer-review journals; [PLOS ONE has guidelines](https://journals.plos.org/plosone/s/materials-and-software-sharing) that exemplify this new ethic of open science.


### CC3.3 - Example Workflows


### CC3.4 - Software Environments

If end-users cannot install your research software, or any software that it depends on, then your workflow is not reproducible. All computational workflows have software dependencies, ranging from a single programming language’s built-in libraries (as of a specific version) to dozens of third-party libraries that link to system libraries written in other languages. Therefore, it’s critical to identify which dependencies, and what versions of those dependencies, are required to reproduce a claim or result (Piccolo & Frampton 2016). For interpreted (or automatically compiled) languages like R, Python, and Julia, virtual environments allow you to create isolated software environments for each of your research projects: only the dependencies (and versions) necessary for that project will be installed. Virtual environments typically provide a convenient way to install all the dependencies, and the correct versions thereof, automatically. For example, Python’s `pip` package manager can report all the dependencies currently installed in your environment and write that information to a file that can be later used to restore that same environment.

“If moving a computation to a new system, it should be simple and straightforward to set up the environment identically (or nearly so) to that on the original machine(s)” (Davison 2012). This dictum, like making regular backups (CC1.7), can help address the unexpected, like when your computer’s hard drive should fail or you need to re-generate some analysis results quickly and you don’t have access to your original computer. Here are some general guidelines to help make this a reality:

- For a target computing environment, use the established package management system to install software dependencies (Davison 2012). For example, system libraries on an Ubuntu/Debian GNU/Linux system should be installed using `apt` while on Mac OS they should be installed using `homebrew`. In a specific programming language like Python, for example, you should use `pip install` or `conda install` instead of running a `setup.py` script, whenever possible. You should always prefer to use a package management system over installing for source: installation with a package manager will generally be safer, faster, and easier to repeat.

### CC3.5 - Digital Identifiers

### CC3.6 - API Documentation and Minimal Working Examples

### CC3.7 - Consistent and Legible Style

Computer code is primarily meant to be read by humans. It’s not sufficient that it runs without error; it should be easy to read and understand by an independent observer who is familiar with the programming language. In every programming language, there are decisions to be made about whitespace, capitalization, and indentation. Check to see if the programming language you are using has style guidelines; the guidelines for Python, as one example, are encapsulated in [the PEP8 Style Guide for Python Code.](https://peps.python.org/pep-0008/) Research communities and private companies also typically have their own style guides (Scott 2016).

In any language, you and the people who you collaborate with on a single project should agree about naming conventions for functions, classes, and other constructs. Will you use `CamelCaseNaming` or `pothole_case_naming` (Wilson et al. 2014) in compound variable names? Consistent indentation, if not enforced by the language (e.g., Python), and consistent spacing will make editing the code easier, particularly by a third party, which should be desirable for open-source software projects. If consistent style is difficult for you to maintain, possibly because of a large and diverse group of contributors to the code, linting programs can help to automatically enforce style. These programs re-format source code without changing or breaking its functionality and can be integrated with version control tools so as to automatically run when the code is changed.

Key to legible scientific code is the appropriate use of whitespace and parentheses.

Code legibility is also impacted by excessively nested control structures, like nested for loops or nested conditionals, which often manifests as excessive indentation. Nested conditionals could be inverted to allow for off-ramps, i.e., breaking the loop or restarting at the next iteration. Nested for loops are harder to disentangle, but a good strategy is to ensure that the body of each for loop is as short as possible. Preferably, the body of deeply nested for loops consists of a single function call, such that the logic of each nested loop is encapsulated by a separate function. Similarly, if a single line of code gets too long or has too many concepts, e.g.:

```py
# Difficult to read
chosen_times = np.argwhere(np.logical_and(np.logical_and(hdf['time'][:,0] == ts0.year, hdf['time'][:,1] == ts0.month), hdf['time'][:,2] == ts0.day))

# Easier to read
chosen_times = np.argwhere(
    np.logical_and(np.logical_and(
        hdf['time'][:,0] == ts0.year,
        hdf['time'][:,1] == ts0.month),
        hdf['time'][:,2] == ts0.day))
```


### CC3.8 - Clear and Informative Variable Names

Variable names should reveal as much information as possible and appropriate about what they are currently representing. For example, a variable name like `soil_moisture_percent` is much more informative and meaningful than `theta`. The former is a name that could be searched in the documentation, or online, and also indicates the units of a quantity, which could be important. Variable names should signal your intent for the data they represent, e.g., `mean_temperature_by_site`.

It’s also a good idea to avoid defining variable names that are similar to others already defined, like `hydraulic_conductivity` and `hydraulic_conductance` even if, as in this example, the variable names refer to distinct concepts (appending units to these names or perhaps using a composite data structure like an associative array might help to distinguish them). Similarly, the use of a singular loop variable name with a plural collection can be confusing because, in English, singular and plural names are hard to visually distinguish. For example:

	for (layer in layers) {
	  ...
	}

At a glance, and particularly in the body of this for loop, it is easy to confuse one variable (“layer”) for the other (“layers”). This can be particularly difficult for readers for whom English is not their first language.

A related issue arises regarding units. While important and re-used coefficients should be implemented as variables with wide scope, e.g.:

	STEFAN_BOLTZ = 5.67e-8 # Stefan-Boltzmann constant, W m-2 K-4
	...
	longwave_net = STEFAN_BOLTZ * (emis_atm - emis_surf) * temp_k**4

This isn’t always practical or appropriate. In cases where a coefficient is written inline, make sure the units of the quantity are explicitly clear with an accompanying inline comment, e.g.:

temp_correction = (temp_k / 293.15) # 20 deg C as deg K



References
==========

Cassey, P., and T. M. Blackburn. 2006. Reproducibility and repeatability in ecology. BioScience 56 (12):958.

Costello, M. J., and J. Wieczorek. 2014. Best practice for biodiversity data management and publication. Biological Conservation 173:68–73.

Davison, A. 2012. Automated Capture of Experiment Context for Easier Reproducibility in Computational Research. Computing in Science & Engineering 14 (4):48–56.

Drummond, C. 2009. “Replicability is not reproducibility: nor is it good science,” in Proceedings of the Evaluation Methods for Machine Learning Workshop at the 26th ICML (Montreal, QC). Available online at: http://www.site.uottawa.ca/~ cdrummon/pubs/ICMLws09.pdf

Goodman, S. N., D. Fanelli, and J. P. A. Ioannidis. 2016. What does research reproducibility mean? Science Translational Medicine 8 (341).

Hutton, C., T. Wagener, J. Freer, D. Han, C. Duffy, and B. Arheimer. 2016. Most computational hydrology is not reproducible, so is it really science? Water Resources Research 52 (10):7548–7555.

Ioannidis, J. P. A. 2005. Why Most Published Research Findings Are False. PLoS Medicine 2 (8):e124.

Michener, W. K. 2015. Ten Simple Rules for Creating a Good Data Management Plan. PLoS Computational Biology. 11(10): e1004525.

Pashler, H., and C. R. Harris. 2012. Is the Replicability Crisis Overblown? Three Arguments Examined. Perspectives on Psychological Science 7 (6):531–536.

Peng, R. D. 2011. Reproducible research in computational science. Science 334 (6060):1226–1227.

Peng, R. D., and S. C. Hicks. 2021. Reproducible research: A retrospective. Annual Review of Public Health 42 (1):79–93.

Piccolo, S. R., and M. B. Frampton. 2016. Tools and techniques for computational reproducibility. GigaScience 5 (1):30.

Rougier, N. P., K. Hinsen, F. Alexandre, T. Arildsen, L. A. Barba, F. C. Y. Benureau, C. T. Brown, P. De Buyl, O. Caglayan, A. P. Davison, M.-A. Delsuc, G. Detorakis, A. K. Diem, D. Drix, P. Enel, B. Girard, O. Guest, M. G. Hall, R. N. Henriques, X. Hinaut, K. S. Jaron, M. Khamassi, A. Klein, T. Manninen, P. Marchesi, D. McGlinn, C. Metzner, O. Petchey, H. E. Plesser, T. Poisot, K. Ram, Y. Ram, E. Roesch, C. Rossant, V. Rostami, A. Shifman, J. Stachelek, M. Stimberg, F. Stollmeier, F. Vaggi, G. Viejo, J. Vitay, A. E. Vostinar, R. Yurchak, and T. Zito. 2017. Sustainable computational science: the ReScience initiative. PeerJ Computer Science 3:e142.

Sandve, G. K., A. Nekrutenko, J. Taylor, and E. Hovig. 2013. Ten Simple Rules for Reproducible Computational Research ed. P. E. Bourne. PLoS Computational Biology 9 (10):e1003285.

Stodden, V., and S. Miguez. 2014. Best practices for computational science: Software infrastructure and environments for reproducible and extensible research. Journal of Open Research Software 2 (1):e21.

Van den Eynden, Veerle, et al. "Managing and sharing data; a best practice guide for researchers." (2011). 3rd edition. https://repository.essex.ac.uk/2156/1/managingsharing.pdf Accessed: June 12, 2023.
