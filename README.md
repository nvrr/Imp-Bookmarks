i created input fields as row and withadd button i add multiple row but i want them independent of each other and can tract their values in js reactjs github:

1.  https://www.codewithfaraz.com/content/8/how-to-create-form-fields-dynamically-with-javascript#google_vignette
2.  https://dev.to/okafor__mary/how-to-dynamically-add-input-fields-on-button-click-in-reactjs-5298   & codeSandbox: https://codesandbox.io/p/sandbox/how-to-dynamically-add-input-fields-by-button-clicl-3jqtww?file=%2Fsrc%2FAddInputFields.js%3A19%2C31
3.  for Table fields:  https://ux.stackexchange.com/questions/112612/how-to-design-an-add-n-rows-button

import React, { useState, useCallback, useMemo } from "react";
import { Button } from "@/components/ui/button";
import { Card } from "@/components/ui/card";

const DynamicInputFields = () => {
  const [rows, setRows] = useState([]);

  const availableOptions = useMemo(() => ["Option 1", "Option 2", "Option 3", "Option 4"], []);

  const addRow = useCallback(() => {
    setRows(prevRows => [...prevRows, { id: Date.now(), selectedOption: "", textValue: "" }]);
  }, []);

  const removeRow = useCallback((id) => {
    setRows(prevRows => prevRows.filter(row => row.id !== id));
  }, []);

  const handleInputChange = useCallback((id, field, value) => {
    setRows(prevRows => prevRows.map(row => (row.id === id ? { ...row, [field]: value } : row)));
  }, []);

  const getDisabledOptions = useCallback((id) => {
    const selectedOptions = rows.filter(row => row.id !== id).map(row => row.selectedOption);
    return availableOptions.filter(option => selectedOptions.includes(option));
  }, [rows, availableOptions]);

  return (
    <div className="p-4 space-y-4">
      {rows.map(row => (
        <Card key={row.id} className="p-4 flex items-center gap-4">
          <select
            className="border p-2 rounded"
            value={row.selectedOption}
            onChange={(e) => handleInputChange(row.id, "selectedOption", e.target.value)}
          >
            <option value="">Select Option</option>
            {availableOptions.map(option => (
              <option
                key={option}
                value={option}
                disabled={getDisabledOptions(row.id).includes(option)}
              >
                {option}
              </option>
            ))}
          </select>
          <input
            type="text"
            className="border p-2 rounded"
            value={row.textValue}
            onChange={(e) => handleInputChange(row.id, "textValue", e.target.value)}
            placeholder="Enter text"
          />
          <Button onClick={() => removeRow(row.id)}>Remove</Button>
        </Card>
      ))}
      <Button onClick={addRow}>Add Row</Button>
    </div>
  );
};

export default DynamicInputFields;
---------------------------------------------------------------------------------------------------------------------------------------
country -> state fields depend on each
https://codesandbox.io/embed/formik-example-3jfxh?fontsize=14&hidenavigation=1&theme=dark

----------------------------------------------------------------------------------------------
i have select field with options based on selected option i create input fields and add button to 
create multiple field rows, i want to disable selected option in another row creation in js reactjs:

import React, { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card } from "@/components/ui/card";

const DynamicInputFields = () => {
  const [rows, setRows] = useState([{ id: Date.now(), selectedOption: "" }]);
  const availableOptions = ["Option 1", "Option 2", "Option 3", "Option 4"];

  const addRow = () => {
    setRows([...rows, { id: Date.now(), selectedOption: "" }]);
  };

  const handleOptionChange = (id, value) => {
    setRows(rows.map(row => (row.id === id ? { ...row, selectedOption: value } : row)));
  };

  const getDisabledOptions = (id) => {
    const selectedOptions = rows.filter(row => row.id !== id).map(row => row.selectedOption);
    return availableOptions.filter(option => selectedOptions.includes(option));
  };

  return (
    <div className="p-4 space-y-4">
      {rows.map(row => (
        <Card key={row.id} className="p-4 flex items-center gap-4">
          <select
            className="border p-2 rounded"
            value={row.selectedOption}
            onChange={(e) => handleOptionChange(row.id, e.target.value)}
          >
            <option value="">Select Option</option>
            {availableOptions.map(option => (
              <option
                key={option}
                value={option}
                disabled={getDisabledOptions(row.id).includes(option)}
              >
                {option}
              </option>
            ))}
          </select>
        </Card>
      ))}
      <Button onClick={addRow}>Add Row</Button>
    </div>
  );
};

export default DynamicInputFields;


-------------------------------------------------or--------------or-----------------or-----------------------------------------

import React, { useState, useCallback } from "react";
import { Button } from "@/components/ui/button";
import { Card } from "@/components/ui/card";

const DynamicInputFields = () => {
  const [rows, setRows] = useState([{ id: Date.now(), selectedOption: "" }]);
  const availableOptions = ["Option 1", "Option 2", "Option 3", "Option 4"];

  const addRow = useCallback(() => {
    setRows(prevRows => [...prevRows, { id: Date.now(), selectedOption: "" }]);
  }, []);

  const removeRow = useCallback((id) => {
    setRows(prevRows => prevRows.filter(row => row.id !== id));
  }, []);

  const handleOptionChange = useCallback((id, value) => {
    setRows(prevRows => prevRows.map(row => (row.id === id ? { ...row, selectedOption: value } : row)));
  }, []);

  const getDisabledOptions = (id) => {
    const selectedOptions = rows.filter(row => row.id !== id).map(row => row.selectedOption);
    return availableOptions.filter(option => selectedOptions.includes(option));
  };

  return (
    <div className="p-4 space-y-4">
      {rows.map(row => (
        <Card key={row.id} className="p-4 flex items-center gap-4">
          <select
            className="border p-2 rounded"
            value={row.selectedOption}
            onChange={(e) => handleOptionChange(row.id, e.target.value)}
          >
            <option value="">Select Option</option>
            {availableOptions.map(option => (
              <option
                key={option}
                value={option}
                disabled={getDisabledOptions(row.id).includes(option)}
              >
                {option}
              </option>
            ))}
          </select>
          <Button onClick={() => removeRow(row.id)}>Remove</Button>
        </Card>
      ))}
      <Button onClick={addRow}>Add Row</Button>
    </div>
  );
};

export default DynamicInputFields;
---------------------------------------------------------------------------------------------------------------------------------------

i have row of fields have select field  in which i want to make priority order , when add, delete rows 
i want remaing to follow priority of order to display one after another ..
priority order is set to one of select filed options based them i want code in reactjs


import React, { useState, useCallback, useMemo } from "react";
import { Button } from "@/components/ui/button";
import { Card } from "@/components/ui/card";

const DynamicInputFields = () => {
  const [rows, setRows] = useState([]);
  const availableOptions = useMemo(() => ["Priority 1", "Priority 2", "Priority 3", "Priority 4"], []);

  const addRow = useCallback(() => {
    setRows(prevRows => {
      const newRow = { id: Date.now(), selectedOption: "", textValue: "", priority: prevRows.length + 1 };
      return [...prevRows, newRow];
    });
  }, []);

  const removeRow = useCallback((id) => {
    setRows(prevRows => {
      const filteredRows = prevRows.filter(row => row.id !== id);
      return filteredRows.map((row, index) => ({ ...row, priority: index + 1 }));
    });
  }, []);

  const handleInputChange = useCallback((id, field, value) => {
    setRows(prevRows => prevRows.map(row => (row.id === id ? { ...row, [field]: value } : row)));
  }, []);

  const getDisabledOptions = useCallback((id) => {
    const selectedOptions = rows.filter(row => row.id !== id).map(row => row.selectedOption);
    return availableOptions.filter(option => selectedOptions.includes(option));
  }, [rows, availableOptions]);

  return (
    <div className="p-4 space-y-4">
      {rows.sort((a, b) => a.priority - b.priority).map(row => (
        <Card key={row.id} className="p-4 flex items-center gap-4">
          <span>Priority {row.priority}</span>
          <select
            className="border p-2 rounded"
            value={row.selectedOption}
            onChange={(e) => handleInputChange(row.id, "selectedOption", e.target.value)}
          >
            <option value="">Select Option</option>
            {availableOptions.map(option => (
              <option
                key={option}
                value={option}
                disabled={getDisabledOptions(row.id).includes(option)}
              >
                {option}
              </option>
            ))}
          </select>
          <input
            type="text"
            className="border p-2 rounded"
            value={row.textValue}
            onChange={(e) => handleInputChange(row.id, "textValue", e.target.value)}
            placeholder="Enter text"
          />
          <Button onClick={() => removeRow(row.id)}>Remove</Button>
        </Card>
      ))}
      <Button onClick={addRow}>Add Row</Button>
    </div>
  );
};

export default DynamicInputFields;


