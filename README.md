# Tech Talent Recruiting with Regex (Python)

**Background:** As a Data Analyst at a leading global HR consultancy, your mission is to delve into an extensive database of resumes to identify suitable candidates for tech-focused roles. This task involves using regular expressions to extract key data points and applying data preprocessing techniques to organize this information effectively.

**Objectives:** Through the application of regular expressions & data preprocessing skills to efficiently organize resume data, a new DataFrame needs to be generated containing the following columns. Only records that are complete & do not contain null or empty string values across these columns should be kept.
- `id`: Candidate ID.
- `job_title`: Most recent job title.
- `tech_skills`: List of technical skills that may include Python, SQL, R, and Excel.
- `education`: Highest educational degree such as PhD, Master, or Bachelor.

This project was done in October, 2025.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Brief Summary
This project utilizes preprocessing techniques to analyze text data & extract particular pieces of information that can help locate suitable candidates for tech-focused roles. The database available provided a vast number of resumes to parse. As such, it was necessary to utilize regular expressions & other preprocessing techniques to retrieve the desired data & transform it into a more organized dataset for the purposes of analysis & more thorough hiring processes.

After the resume data was imported, it was explored at a basic level to determine what kind of problems & inconsistencies were present. Knowing such information was informative in understanding what preprocessing steps were necessary in addition to how the variables might need to be manipulated in order to retrieve the desired information.  
Fortunately, this brief evaluation of the 1,352 candidate records did not find any significant impediments that required initial preprocessing.

In order to obtain the desired information, the provided dataset had to be evaluated to learn how to do so. Retrieving the candidate ID was simple given that it was present in the original dataset. When it came to finding candidates' most recent job title, relevant technical skills, & the highest degree they obtained, the resume data had to be parsed fairly liberally.

#### Investigating the Resumes
The resume data was investigated extensively to determine how to retrieve the desired information; however, given that there were 1,352 resumes, analyzing them all was unreasonable. As such, a few dozen random resumes were sampled & evaluated for commonalities & differences that might make obtaining the desired information easier. Ultimately, this examination revealed that there is an overall general format to this variable; however, parsing it & easily extracting the desired data would not be simple.  
Generally, a resume begins with a fully capitalized job title, some of which are vague (e.g. "SALES"), followed by an indent. Furthermore, some resumes contained unusual characters within these fully capitalized words/word sequences such as "\n" (indicating a new line). This information was taken to refer to a candidate's most recent job title.

Following this first detail, there are a plethora of other inconsistencies that prevent any single preprocessing technique from being applied such as different section headers, different separators, repeated sections, & more.  
Ultimately, the objectives in this project defined describe specific variables including pieces of information to look for within the resumes. Given that the two remaining variables look for particular details in a resume, regular expressions ("regex" patterns) were utilized to look for & extract such patterns.

#### Compiling the Desired Information
To apply regular expressions, functions from the `re` module were used. As mentioned previously, the candidate ID was obtained straight from the original dataset. The most recent job title was also established to be the fully capitalized text at the beginning of each resume. As such, the `re.search()` function was used to search for such text; the specific pattern can be found in **Analysis I**.

For the technical skills, `re.findall()` was used to look for mentions of Python, Excel, R &/or SQL in a resume regardless of capitalization. If other technical skills become relevant or requisites for certain tech jobs, they could be added to this pattern.

Next, resumes were parsed to look for any educational degrees obtained by a candidate using the `re.findall()` function. To form these lookups, the following degrees & education levels were used: PhD, Doctoral, Masters, Bachelors, Associates, High School. Others could be added to this pattern if relevant.  
Many resumes listed multiple educational accomplishments. To determine the highest level obtained, additional processing had to be employed. Firstly, the order of these levels had to be established. In this project, this educational hierarchy was defined, from highest to lowest, as: "Doctoral/PhD," "Master/Masters/MCS," "Bachelor/Bachelors/BCS," "Associates," "High School."

Another requirement in the analysis involved eliminating resumes that did not have information pertaining to a candidate's most recent job title, technical skills, or educational accomplishments. The application of this rule truncated the number of suitable candidates from 1,352 to 444. This missingness could be attributed to a candidate not listing the relevant information in their resume either because they did not possess/achieve it or because they simply did not think to include it.

By applying regular expressions & other coding constructs, like for loops, the desired information was obtained & neatly organized into a table; `candidates_df`. If additional requisites for tech-focused roles want to be introduced in hiring processes, additional patterns can be built to find fitting candidates.
