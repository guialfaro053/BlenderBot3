# How to run BlenderBot3 3B

 1. **Clone ParlAI repository and install ParlAI**:
        `git clone https://github.com/facebookresearch/ParlAI.git ~/ParlAI`
        `cd ~/ParlAI; python setup.py develop`
        Several problems can arise when running the latter comand. Most of the problems are related to CUDA compatibility problems. The installation was tested on Windows, Mac, and Linux, from which only Linux had no problems during installation. <del> Also, `pip install parlai` although it does install all ParlAI instances, it has not been fully updated, and thus, it does not run BB3 yet. </del>.
  
 2. **Running BlenderBot3**:
		BlenderBot3 can now be used by running `parlai interactive --model-file zoo:bb3/bb3_3B/model --init-opt gen/r2c2_bb3`, but we found it to present "ConnectionError HTTPConnectionPool" problems, and thus, unstable to converse.  We recommend using the command shown on the [model zoo](https://www.parl.ai/docs/zoo.html) list on ParlAI where a server for internet queries is included. The command now becomes: `parlai i -mf zoo:bb3/bb3_3B/model -o gen/r2c2_bb3 --search-server relevant_search_server`.
		
 3. **Setting a server for BlenderBot3**:
        We found that many times the server connection for internet queries was slow and unstable. Hence, we recommend using a search engine for ParlAI.  The repository [ParlAI_SearchEngine](https://github.com/freakeinstein/ParlAI_SearchEngine) shows a way to use one. Start by cloning the repo `git clone https://github.com/freakeinstein/ParlAI_SearchEngine.git`. Although the requirements.txt file automatically installs all necessary pip libraries, there were some conflicts with the versions installed and ParlAI (this is because the serach engine is used for BlenderBot2), so we recommend to pip install only the necessary libraries presented in the file. It is possible to access to three different search engines. Despite Google is the default server, we found it to be slow and prone to connection errors. The fastest and more stable engine was Aquila. You can access to the server by running `python search_server.py serve --host 0.0.0.0:8080 --search_engine="Aquila" --subscription_key "put your Aquila public key here"`. Finally, run  BlenderBot3 with the following command: `parlai i -mf zoo:bb3/bb3_3B/model -o gen/r2c2_bb3 --search-server 0.0.0.0:8080`.
